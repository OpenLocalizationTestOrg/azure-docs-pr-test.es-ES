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
# <a name="transactions-in-sql-data-warehouse"></a>Transacciones en el Almacenamiento de datos SQL
Como cabría esperar, almacenamiento de datos SQL admite transacciones como parte de la carga de trabajo de almacenamiento de datos de Hola. Sin embargo, rendimiento de hello tooensure de almacenamiento de datos de SQL se mantiene a escala que algunas características están limitadas cuando comparado tooSQL Server. Este artículo resalta las diferencias de Hola y Hola listas de otros usuarios. 

## <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacciones
El Almacenamiento de datos SQL implementa las transacciones ACID. Sin embargo, aislamiento de compatibilidad transaccional Hola Hola se limita demasiado`READ UNCOMMITTED` y no puede cambiarse. Puede implementar una serie de métodos de codificación tooprevent desfasada lee de datos si se trata de un problema para usted. Hello más populares métodos aprovechan CTAS y modificación de particiones de tabla (a menudo conocido como Hola patrón de ventana deslizante) tooprevent a los usuarios de consultar los datos aún se está preparando. Vistas que filtran previamente los datos de hello también es un enfoque popular.  

## <a name="transaction-size"></a>Tamaño de la transacción
Una transacción de modificación de datos única tiene un tamaño limitado. Hola hoy en día se aplique el límite "por distribución". Por lo tanto, se puede calcular la asignación total Hola multiplicando el límite de Hola por recuento de distribución de Hola. número máximo de hello tooapproximate de filas de la transacción de hello divide cap de distribución de Hola por tamaño total de Hola de cada fila. Columnas de longitud variable considere la posibilidad de tomar una longitud de la columna promedio, en lugar de usar tamaño máximo de Hola.

En la tabla Hola Hola se realizaron suposiciones siguientes:

* Se ha producido una distribución uniforme de los datos 
* longitud media de fila de Hello es 250 bytes

| [DWU][DWU] | Extremo por distribución (GiB) | Número de distribuciones | Tamaño máximo de la transacción (GiB) | # Filas por distribución | Máximo de filas por transacción |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4 000 000 |240 000 000 |
| DW200 |1.5 |60 |90 |6.000.000 |360 000 000 |
| DW300 |2.25 |60 |135 |9 000 000 |540 000 000 |
| DW400 |3 |60 |180 |12 000 000 |720 000 000 |
| DW500 |3,75 |60 |225 |15 000 000 |900 000 000 |
| DW600 |4.5. |60 |270 |18 000 000 |1 080 000 000 |
| DW1000 |7.5 |60 |450 |30 000 000 |1 800 000 000 |
| DW1200 |9 |60 |540 |36 000 000 |2 160 000 000 |
| DW1500 |11,25 |60 |675 |45 000 000 |2 700 000 000 |
| DW2000 |15 |60 |900 |60 000 000 |3 600 000 000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

límite de tamaño de transacción de Hola se aplica por transacción u operación. No se aplica en todas las transacciones simultáneas. Por lo tanto, cada transacción está permitido toowrite esta cantidad de datos toohello registro. 

toooptimize y minimizar la cantidad de Hola de los datos escritos toohello registro consulte toohello [prácticas recomendadas de las transacciones] [ Transactions best practices] artículo.

> [!WARNING]
> Hola máximo tamaño de las transacciones solo se pueden conseguir para HASH o tablas ROUND_ROBIN distribuidas donde propagarse Hola Hola datos es par. Si transacción Hola está escribiendo datos en un modo sesgado distribuciones toohello, a continuación, hello límite es probable toobe alcanzado el tamaño máximo de la transacción de toohello anteriores.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Estado de las transacciones
Almacenamiento de datos de SQL utiliza hello xact_state función tooreport una transacción errónea con hello valor -2. Esto significa que transacción Hola ha fallado y se marca para la reversión solo

> [!NOTE]
> Hola el uso de -2 por hello XACT_STATE función toodenote un comportamiento diferente de representa transacción errónea tooSQL Server. SQL Server utiliza el valor -1 de hello toorepresent una transacción no confirmable. SQL Server puede tolerar algunos errores dentro de una transacción sin necesidad de toobe marcado como no confirmable. Por ejemplo, `SELECT 1/0` producirá un error pero no fuerza una transacción en un estado no confirmable. SQL Server también permite a las lecturas de transacción no confirmable Hola. Sin embargo, Almacenamiento de datos SQL no permite hacerlo. Si se produce un error dentro de una transacción de almacenamiento de datos SQL se pasará automáticamente al estado de hello -2 y no será capaz de toomake cualquiera más instrucciones select hasta que se ha revertido instrucción Hola. Por lo tanto es toocheck importante que su toosee de código de aplicación si usa xact_state que puede requerir modificaciones en el código toomake.
> 
> 

Por ejemplo, puede que vea una transacción con el siguiente aspecto en SQL Server:

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

Si deja el código tal cual está por encima obtendrá Hola mensaje de error siguiente:

Msg 111233, nivel 16, estado 1, línea 1 111233; Hola actual anuló la transacción y los cambios pendientes se han revertido. Causa: una transacción en estado de solo reversión no se ha revertido explícitamente antes de la instrucción DDL, DML o SELECT.

También puede obtener no salida Hola de hello error. * funciones.

En el almacén de datos de SQL código de hello necesita toobe ligeramente modificado:

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

Hola espera ahora se observa el comportamiento. se administra el error de Hello en transacciones de Hola y Hola error. * funciones que proporcionan valores según lo previsto.

Todo lo que ha cambiado es ese hello `ROLLBACK` de hello transacción tenía toohappen antes de que Hola de lectura de la información de error de Hola Hola `CATCH` bloque.

## <a name="errorline-function"></a>Función Error_Line()
También merece la pena destacar que almacenamiento de datos SQL no implementar admitir o función de hello error_line (). Si tiene esto en el código debe tooremove toobe compatible con el almacenamiento de datos de SQL. Usar etiquetas de consulta en el código en su lugar tooimplement una funcionalidad equivalente. Consulte toohello [etiqueta] [ LABEL] artículo para obtener más información acerca de esta característica.

## <a name="using-throw-and-raiserror"></a>Uso de THROW y RAISERROR
THROW es Hola implementación más moderno para generar excepciones en el almacén de datos de SQL pero RAISERROR también se admite. Hay algunas diferencias que son vale la pena prestar atención toohowever.

* Números no pueden estar en hello 100.000 150.000 intervalo para THROW de mensajes de error definidos por el usuario
* Los mensajes de error RAISERROR se fijan en 50.000.
* No se admite el uso de sys.messages.

## <a name="limitiations"></a>Limitaciones
Almacenamiento de datos de SQL tiene algunas otras restricciones que se relacionan tootransactions.

Los pasos son los siguientes:

* Transacciones no distribuidas
* Transacciones anidadas no permitidas
* Puntos de almacenamiento no admitidos
* Sin transacciones con nombre
* Sin transacciones marcadas
* No existe compatibilidad con DDL como el elemento `CREATE TABLE` de una transacción definida por el usuario

## <a name="next-steps"></a>Pasos siguientes
toolearn más acerca de cómo optimizar las transacciones, vea [prácticas recomendadas de las transacciones][Transactions best practices].  toolearn sobre otras prácticas recomendadas de almacenamiento de datos SQL, consulte [prácticas recomendadas de almacenamiento de datos SQL][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
