---
title: Transacciones en SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="73231-103">Transacciones en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="73231-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="73231-104">Como cabría esperar, el Almacenamiento de datos SQL admite transacciones como parte de la carga de trabajo de dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="73231-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="73231-105">Sin embargo, para garantizar que se mantiene a escala el rendimiento del Almacenamiento de datos SQL, algunas características están limitadas en comparación con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="73231-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="73231-106">En este artículo se destacan las diferencias entre las características y se enumeran las demás.</span><span class="sxs-lookup"><span data-stu-id="73231-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="73231-107">Niveles de aislamiento de transacciones</span><span class="sxs-lookup"><span data-stu-id="73231-107">Transaction isolation levels</span></span>
<span data-ttu-id="73231-108">El Almacenamiento de datos SQL implementa las transacciones ACID.</span><span class="sxs-lookup"><span data-stu-id="73231-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="73231-109">Sin embargo, el aislamiento de la compatibilidad transaccional está limitado a `READ UNCOMMITTED` y no puede cambiarse.</span><span class="sxs-lookup"><span data-stu-id="73231-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="73231-110">Puede implementar una serie de métodos para evitar lecturas de datos sucios si esto le plantea alguna preocupación.</span><span class="sxs-lookup"><span data-stu-id="73231-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="73231-111">Los métodos más populares utilizan CTAS y la modificación de particiones de tabla (que suele conocerse como un patrón de ventana deslizante) para evitar que los usuarios consulten datos que aún se encuentran en fase de preparación.</span><span class="sxs-lookup"><span data-stu-id="73231-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="73231-112">Las vistas que filtran los datos previamente también constituyen un enfoque popular.</span><span class="sxs-lookup"><span data-stu-id="73231-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="73231-113">Tamaño de la transacción</span><span class="sxs-lookup"><span data-stu-id="73231-113">Transaction size</span></span>
<span data-ttu-id="73231-114">Una transacción de modificación de datos única tiene un tamaño limitado.</span><span class="sxs-lookup"><span data-stu-id="73231-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="73231-115">Actualmente, el límite se aplica "por distribución".</span><span class="sxs-lookup"><span data-stu-id="73231-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="73231-116">Por lo tanto, la asignación total puede calcularse multiplicando el límite por el recuento de distribución.</span><span class="sxs-lookup"><span data-stu-id="73231-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="73231-117">Para aproximar el número máximo de filas de la transacción, divida el extremo de la distribución entre el tamaño total de cada fila.</span><span class="sxs-lookup"><span data-stu-id="73231-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="73231-118">Para las columnas de longitud variable, en lugar de utilizar el tamaño máximo, tenga en cuenta la longitud media de la columna.</span><span class="sxs-lookup"><span data-stu-id="73231-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="73231-119">En la tabla siguiente se han considerado estas hipótesis:</span><span class="sxs-lookup"><span data-stu-id="73231-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="73231-120">Se ha producido una distribución uniforme de los datos</span><span class="sxs-lookup"><span data-stu-id="73231-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="73231-121">La longitud media de la fila es de 250 bytes</span><span class="sxs-lookup"><span data-stu-id="73231-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="73231-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="73231-122">[DWU][DWU]</span></span> | <span data-ttu-id="73231-123">Extremo por distribución (GiB)</span><span class="sxs-lookup"><span data-stu-id="73231-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="73231-124">Número de distribuciones</span><span class="sxs-lookup"><span data-stu-id="73231-124">Number of Distributions</span></span> | <span data-ttu-id="73231-125">Tamaño máximo de la transacción (GiB)</span><span class="sxs-lookup"><span data-stu-id="73231-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="73231-126"># Filas por distribución</span><span class="sxs-lookup"><span data-stu-id="73231-126"># Rows per distribution</span></span> | <span data-ttu-id="73231-127">Máximo de filas por transacción</span><span class="sxs-lookup"><span data-stu-id="73231-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="73231-128">DW100</span><span class="sxs-lookup"><span data-stu-id="73231-128">DW100</span></span> |<span data-ttu-id="73231-129">1</span><span class="sxs-lookup"><span data-stu-id="73231-129">1</span></span> |<span data-ttu-id="73231-130">60</span><span class="sxs-lookup"><span data-stu-id="73231-130">60</span></span> |<span data-ttu-id="73231-131">60</span><span class="sxs-lookup"><span data-stu-id="73231-131">60</span></span> |<span data-ttu-id="73231-132">4 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-132">4,000,000</span></span> |<span data-ttu-id="73231-133">240 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-133">240,000,000</span></span> |
| <span data-ttu-id="73231-134">DW200</span><span class="sxs-lookup"><span data-stu-id="73231-134">DW200</span></span> |<span data-ttu-id="73231-135">1.5</span><span class="sxs-lookup"><span data-stu-id="73231-135">1.5</span></span> |<span data-ttu-id="73231-136">60</span><span class="sxs-lookup"><span data-stu-id="73231-136">60</span></span> |<span data-ttu-id="73231-137">90</span><span class="sxs-lookup"><span data-stu-id="73231-137">90</span></span> |<span data-ttu-id="73231-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="73231-138">6,000,000</span></span> |<span data-ttu-id="73231-139">360 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-139">360,000,000</span></span> |
| <span data-ttu-id="73231-140">DW300</span><span class="sxs-lookup"><span data-stu-id="73231-140">DW300</span></span> |<span data-ttu-id="73231-141">2.25</span><span class="sxs-lookup"><span data-stu-id="73231-141">2.25</span></span> |<span data-ttu-id="73231-142">60</span><span class="sxs-lookup"><span data-stu-id="73231-142">60</span></span> |<span data-ttu-id="73231-143">135</span><span class="sxs-lookup"><span data-stu-id="73231-143">135</span></span> |<span data-ttu-id="73231-144">9 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-144">9,000,000</span></span> |<span data-ttu-id="73231-145">540 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-145">540,000,000</span></span> |
| <span data-ttu-id="73231-146">DW400</span><span class="sxs-lookup"><span data-stu-id="73231-146">DW400</span></span> |<span data-ttu-id="73231-147">3</span><span class="sxs-lookup"><span data-stu-id="73231-147">3</span></span> |<span data-ttu-id="73231-148">60</span><span class="sxs-lookup"><span data-stu-id="73231-148">60</span></span> |<span data-ttu-id="73231-149">180</span><span class="sxs-lookup"><span data-stu-id="73231-149">180</span></span> |<span data-ttu-id="73231-150">12 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-150">12,000,000</span></span> |<span data-ttu-id="73231-151">720 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-151">720,000,000</span></span> |
| <span data-ttu-id="73231-152">DW500</span><span class="sxs-lookup"><span data-stu-id="73231-152">DW500</span></span> |<span data-ttu-id="73231-153">3,75</span><span class="sxs-lookup"><span data-stu-id="73231-153">3.75</span></span> |<span data-ttu-id="73231-154">60</span><span class="sxs-lookup"><span data-stu-id="73231-154">60</span></span> |<span data-ttu-id="73231-155">225</span><span class="sxs-lookup"><span data-stu-id="73231-155">225</span></span> |<span data-ttu-id="73231-156">15 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-156">15,000,000</span></span> |<span data-ttu-id="73231-157">900 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-157">900,000,000</span></span> |
| <span data-ttu-id="73231-158">DW600</span><span class="sxs-lookup"><span data-stu-id="73231-158">DW600</span></span> |<span data-ttu-id="73231-159">4.5.</span><span class="sxs-lookup"><span data-stu-id="73231-159">4.5</span></span> |<span data-ttu-id="73231-160">60</span><span class="sxs-lookup"><span data-stu-id="73231-160">60</span></span> |<span data-ttu-id="73231-161">270</span><span class="sxs-lookup"><span data-stu-id="73231-161">270</span></span> |<span data-ttu-id="73231-162">18 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-162">18,000,000</span></span> |<span data-ttu-id="73231-163">1 080 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-163">1,080,000,000</span></span> |
| <span data-ttu-id="73231-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="73231-164">DW1000</span></span> |<span data-ttu-id="73231-165">7.5</span><span class="sxs-lookup"><span data-stu-id="73231-165">7.5</span></span> |<span data-ttu-id="73231-166">60</span><span class="sxs-lookup"><span data-stu-id="73231-166">60</span></span> |<span data-ttu-id="73231-167">450</span><span class="sxs-lookup"><span data-stu-id="73231-167">450</span></span> |<span data-ttu-id="73231-168">30 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-168">30,000,000</span></span> |<span data-ttu-id="73231-169">1 800 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-169">1,800,000,000</span></span> |
| <span data-ttu-id="73231-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="73231-170">DW1200</span></span> |<span data-ttu-id="73231-171">9</span><span class="sxs-lookup"><span data-stu-id="73231-171">9</span></span> |<span data-ttu-id="73231-172">60</span><span class="sxs-lookup"><span data-stu-id="73231-172">60</span></span> |<span data-ttu-id="73231-173">540</span><span class="sxs-lookup"><span data-stu-id="73231-173">540</span></span> |<span data-ttu-id="73231-174">36 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-174">36,000,000</span></span> |<span data-ttu-id="73231-175">2 160 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-175">2,160,000,000</span></span> |
| <span data-ttu-id="73231-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="73231-176">DW1500</span></span> |<span data-ttu-id="73231-177">11,25</span><span class="sxs-lookup"><span data-stu-id="73231-177">11.25</span></span> |<span data-ttu-id="73231-178">60</span><span class="sxs-lookup"><span data-stu-id="73231-178">60</span></span> |<span data-ttu-id="73231-179">675</span><span class="sxs-lookup"><span data-stu-id="73231-179">675</span></span> |<span data-ttu-id="73231-180">45 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-180">45,000,000</span></span> |<span data-ttu-id="73231-181">2 700 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-181">2,700,000,000</span></span> |
| <span data-ttu-id="73231-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="73231-182">DW2000</span></span> |<span data-ttu-id="73231-183">15</span><span class="sxs-lookup"><span data-stu-id="73231-183">15</span></span> |<span data-ttu-id="73231-184">60</span><span class="sxs-lookup"><span data-stu-id="73231-184">60</span></span> |<span data-ttu-id="73231-185">900</span><span class="sxs-lookup"><span data-stu-id="73231-185">900</span></span> |<span data-ttu-id="73231-186">60 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-186">60,000,000</span></span> |<span data-ttu-id="73231-187">3 600 000 000</span><span class="sxs-lookup"><span data-stu-id="73231-187">3,600,000,000</span></span> |
| <span data-ttu-id="73231-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="73231-188">DW3000</span></span> |<span data-ttu-id="73231-189">22.5</span><span class="sxs-lookup"><span data-stu-id="73231-189">22.5</span></span> |<span data-ttu-id="73231-190">60</span><span class="sxs-lookup"><span data-stu-id="73231-190">60</span></span> |<span data-ttu-id="73231-191">1,350</span><span class="sxs-lookup"><span data-stu-id="73231-191">1,350</span></span> |<span data-ttu-id="73231-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="73231-192">90,000,000</span></span> |<span data-ttu-id="73231-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="73231-193">5,400,000,000</span></span> |
| <span data-ttu-id="73231-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="73231-194">DW6000</span></span> |<span data-ttu-id="73231-195">45</span><span class="sxs-lookup"><span data-stu-id="73231-195">45</span></span> |<span data-ttu-id="73231-196">60</span><span class="sxs-lookup"><span data-stu-id="73231-196">60</span></span> |<span data-ttu-id="73231-197">2,700</span><span class="sxs-lookup"><span data-stu-id="73231-197">2,700</span></span> |<span data-ttu-id="73231-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="73231-198">180,000,000</span></span> |<span data-ttu-id="73231-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="73231-199">10,800,000,000</span></span> |

<span data-ttu-id="73231-200">Se aplica el límite de tamaño de la transacción por transacción u operación.</span><span class="sxs-lookup"><span data-stu-id="73231-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="73231-201">No se aplica en todas las transacciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="73231-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="73231-202">Por tanto, cada transacción puede escribir esta cantidad de datos en el registro.</span><span class="sxs-lookup"><span data-stu-id="73231-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="73231-203">Para optimizar y minimizar la cantidad de datos que se escriben en el registro, consulte el artículo sobre [procedimientos recomendados relacionados con las transacciones][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="73231-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="73231-204">El tamaño máximo de la transacción solo se puede conseguir para las tablas de distribución HASH o ROUND_ROBIN donde la propagación de los datos es uniforme.</span><span class="sxs-lookup"><span data-stu-id="73231-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="73231-205">Si la transacción está escribiendo datos de forma sesgada en las distribuciones, es posible que el límite se alcance antes de que la transacción llegue al máximo de su tamaño.</span><span class="sxs-lookup"><span data-stu-id="73231-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="73231-206">Estado de las transacciones</span><span class="sxs-lookup"><span data-stu-id="73231-206">Transaction state</span></span>
<span data-ttu-id="73231-207">El Almacenamiento de datos SQL usa la función XACT_STATE() para notificar una transacción errónea con el valor -2.</span><span class="sxs-lookup"><span data-stu-id="73231-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="73231-208">Esto significa que se ha producido un error en la transacción y que está marcada para reversión únicamente.</span><span class="sxs-lookup"><span data-stu-id="73231-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="73231-209">El uso de -2 por la función XACT_STATE para denotar una transacción errónea representa un comportamiento diferente para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="73231-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="73231-210">SQL Server utiliza el valor -1 para representar una transacción no confirmable.</span><span class="sxs-lookup"><span data-stu-id="73231-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="73231-211">SQL Server puede tolerar errores dentro de una transacción sin necesidad de que se marque como no confirmable.</span><span class="sxs-lookup"><span data-stu-id="73231-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="73231-212">Por ejemplo, `SELECT 1/0` producirá un error pero no fuerza una transacción en un estado no confirmable.</span><span class="sxs-lookup"><span data-stu-id="73231-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="73231-213">SQL Server también permite lecturas en la transacción no confirmable.</span><span class="sxs-lookup"><span data-stu-id="73231-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="73231-214">Sin embargo, Almacenamiento de datos SQL no permite hacerlo.</span><span class="sxs-lookup"><span data-stu-id="73231-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="73231-215">Si se produce un error dentro de una transacción de Almacenamiento de datos SQL, especificará automáticamente el estado 2 y no podrá realizar más instrucciones select hasta que la instrucción se haya revertido.</span><span class="sxs-lookup"><span data-stu-id="73231-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="73231-216">Por lo tanto, es importante comprobar el código de aplicación para ver si utiliza XACT_STATE() cuando necesite realizar modificaciones de código.</span><span class="sxs-lookup"><span data-stu-id="73231-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="73231-217">Por ejemplo, puede que vea una transacción con el siguiente aspecto en SQL Server:</span><span class="sxs-lookup"><span data-stu-id="73231-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="73231-218">Si deja el código como aparecía anteriormente, obtendrá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="73231-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="73231-219">Msg 111233, Level 16, State 1, Line 1 111233; La transacción actual se ha anulado y se han revertido los cambios pendientes.</span><span class="sxs-lookup"><span data-stu-id="73231-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="73231-220">Causa: una transacción en estado de solo reversión no se ha revertido explícitamente antes de la instrucción DDL, DML o SELECT.</span><span class="sxs-lookup"><span data-stu-id="73231-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="73231-221">Tampoco obtendrá el resultado de las funciones ERROR_*.</span><span class="sxs-lookup"><span data-stu-id="73231-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="73231-222">En el Almacenamiento de datos SQL debe modificarse ligeramente el código:</span><span class="sxs-lookup"><span data-stu-id="73231-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

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

<span data-ttu-id="73231-223">Ahora se observa el comportamiento esperado.</span><span class="sxs-lookup"><span data-stu-id="73231-223">The expected behavior is now observed.</span></span> <span data-ttu-id="73231-224">Se administra el error en la transacción y las funciones ERROR_* proporcionan los valores esperados.</span><span class="sxs-lookup"><span data-stu-id="73231-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="73231-225">Todo lo que ha cambiado es que se tuvo que aplicar `ROLLBACK` de la transacción para leer la información de error en el bloque `CATCH`.</span><span class="sxs-lookup"><span data-stu-id="73231-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="73231-226">Función Error_Line()</span><span class="sxs-lookup"><span data-stu-id="73231-226">Error_Line() function</span></span>
<span data-ttu-id="73231-227">También cabe destacar que el Almacenamiento de datos SQL no implementa o admite la función ERROR_LINE().</span><span class="sxs-lookup"><span data-stu-id="73231-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="73231-228">Si tiene esto en el código, tendrá que eliminarlo para que sea compatible con el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="73231-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="73231-229">En su lugar, utilice etiquetas de consulta en el código para implementar una funcionalidad equivalente.</span><span class="sxs-lookup"><span data-stu-id="73231-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="73231-230">Consulte el artículo sobre [USO DE ETIQUETAS][LABEL] para más información sobre esta característica.</span><span class="sxs-lookup"><span data-stu-id="73231-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="73231-231">Uso de THROW y RAISERROR</span><span class="sxs-lookup"><span data-stu-id="73231-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="73231-232">THROW es la implementación más moderna para producir excepciones en el Almacenamiento de datos SQL, pero también se admite RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="73231-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="73231-233">Sin embargo, hay algunas diferencias a las que se debe prestar atención.</span><span class="sxs-lookup"><span data-stu-id="73231-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="73231-234">Los números de mensajes de error definidos no pueden encontrarse en el intervalo 100.000 a 150.000 para THROW.</span><span class="sxs-lookup"><span data-stu-id="73231-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="73231-235">Los mensajes de error RAISERROR se fijan en 50.000.</span><span class="sxs-lookup"><span data-stu-id="73231-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="73231-236">No se admite el uso de sys.messages.</span><span class="sxs-lookup"><span data-stu-id="73231-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="73231-237">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="73231-237">Limitiations</span></span>
<span data-ttu-id="73231-238">El Almacenamiento de datos SQL tiene algunas otras restricciones relacionadas con las transacciones.</span><span class="sxs-lookup"><span data-stu-id="73231-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="73231-239">Los pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="73231-239">They are as follows:</span></span>

* <span data-ttu-id="73231-240">Transacciones no distribuidas</span><span class="sxs-lookup"><span data-stu-id="73231-240">No distributed transactions</span></span>
* <span data-ttu-id="73231-241">Transacciones anidadas no permitidas</span><span class="sxs-lookup"><span data-stu-id="73231-241">No nested transactions permitted</span></span>
* <span data-ttu-id="73231-242">Puntos de almacenamiento no admitidos</span><span class="sxs-lookup"><span data-stu-id="73231-242">No save points allowed</span></span>
* <span data-ttu-id="73231-243">Sin transacciones con nombre</span><span class="sxs-lookup"><span data-stu-id="73231-243">No named transactions</span></span>
* <span data-ttu-id="73231-244">Sin transacciones marcadas</span><span class="sxs-lookup"><span data-stu-id="73231-244">No marked transactions</span></span>
* <span data-ttu-id="73231-245">No existe compatibilidad con DDL como el elemento `CREATE TABLE` de una transacción definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="73231-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="73231-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73231-246">Next steps</span></span>
<span data-ttu-id="73231-247">Para más información acerca de la optimización de transacciones, consulte [Procedimientos recomendados relacionados con las transacciones][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="73231-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="73231-248">Para más información sobre otros procedimientos recomendados de SQL Data Warehouse, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="73231-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
