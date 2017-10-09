---
title: OLTP aaaIn memoria mejora el rendimiento de transacciones SQL | Documentos de Microsoft
description: OLTP en memoria de adoptar tooimprove performance de las transacciones en una base de datos SQL existente.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Use In-Memory OLTP tooimprove el rendimiento de la aplicación en la base de datos SQL
[OLTP en memoria](sql-database-in-memory.md) puede ser usado tooimprove Hola rendimiento de procesamiento de transacciones, recopilación de datos y los escenarios de datos transitorios, en [Premium](sql-database-service-tiers.md) Hola a bases de datos de SQL de Azure sin aumentar el nivel de precios. 

> [!NOTE] 
> Más información sobre cómo [Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Siga estos pasos tooadopt OLTP en memoria en la base de datos existente.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Paso 1: Asegúrese de estar utilizando una base de datos premium
OLTP en memoria solo se admite en bases de datos premium. Se admite en memoria si Hola devuelve el resultado es 1 (no 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* son las siglas de *Extreme Transaction Processing*.



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Paso 2: Identificar objetos de toomigrate tooIn memoria OLTP
SSMS incluye un informe de **información general del análisis de rendimiento de transacciones** que se pueden ejecutar en una base de datos con una carga de trabajo activo. informe de Hello identifica las tablas y procedimientos almacenados que son candidatos para la migración de OLTP tooIn memoria.

En SSMS, informe de Hola toogenerate:

* Hola **Explorador de objetos**, haga clic en el nodo de base de datos.
* Haga clic en **Informes** > **Informes estándar** > **Información general de análisis de rendimiento de transacciones**.

Para obtener más información, consulte [determinar si una tabla o un procedimiento almacenado debe ser pasar OLTP de memoria tooIn](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Paso 3: Crear una base de datos de prueba comparables
Imagine que informe de hello indica la base de datos ha una tabla que se beneficiaría de la que se va a convertir tabla optimizada en memoria de tooa. Le recomendamos que pruebe en primer lugar indicación de hello tooconfirm probando.

Necesitará una copia de prueba de la base de datos de producción. Hello base de datos de prueba debe ser en hello mismo nivel de servicio como la base de datos de producción.

tooease probar, ajustar la base de datos de prueba como se indica a continuación:

1. Conectar la base de datos de prueba de toohello mediante SSMS.
2. tooavoid necesidad Hola opción WITH (SNAPSHOT) en las consultas, establezca la opción de base de datos de hello como se muestra en hello después de la instrucción T-SQL:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Paso 4: Migrar tablas
Debe crear y rellenar una copia con optimización para memoria de tabla Hola desea tootest. Se puede crear mediante:

* Hola práctica Asistente de optimización de memoria en SSMS.
* T-SQL manual.

#### <a name="memory-optimization-wizard-in-ssms"></a>Asistente para optimización de memoria en SSMS
toouse esta opción de migración:

1. Conectar la base de datos de prueba de toohello con SSMS.
2. Hola **Explorador de objetos**, haga doble clic en la tabla de hello y, a continuación, haga clic en **Memory Optimization Advisor**.
   
   * Hola **Asistente de optimizador de memoria de tablas** se muestra el asistente.
3. En el Asistente de hello, haga clic en **validación migración** (o hello **siguiente** botón) toosee si tabla hello tiene alguna no admite características que no se admiten en tablas optimizadas en memoria. Para más información, consulte:
   
   * Hola *lista de comprobación de optimización de memoria* en [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Construcciones de transact-SQL no admitidas por In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrar OLTP de memoria tooIn](http://msdn.microsoft.com/library/dn247639.aspx).
4. Si Hola tabla no tiene ninguna característica no admitida, Asesor de hello puede realizar esquema real de Hola y migración de datos.

#### <a name="manual-t-sql"></a>T-SQL manual
toouse esta opción de migración:

1. Conectar la base de datos de prueba de tooyour mediante SSMS (o una utilidad similar).
2. Obtenga el script de T-SQL completo de hello para la tabla y sus índices.
   
   * En SSMS, haga clic con el botón derecho en el nodo de tabla.
   * Haga clic en **Incluir tabla como** > **Crear en** > **Nueva ventana de consulta**.
3. En la ventana de script de Hola, agregue WITH (MEMORY_OPTIMIZED = ON) toohello instrucción CREATE TABLE.
4. Si hay un índice agrupado, cámbielo tooNONCLUSTERED.
5. Cambiar el nombre de tabla existente de hello mediante SP_RENAME.
6. Crear copia optimizadas en memoria nueva Hola de tabla de Hola ejecutando el script CREATE TABLE editado.
7. Copiar la tabla optimizada en memoria de hello datos tooyour mediante INSERT... SELECCIONE * EN:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Paso 5 (opcional): Migrar los procedimientos almacenados
característica de Hello en memoria también puede modificar un procedimiento almacenado para mejorar el rendimiento.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Consideraciones con procedimientos almacenados compilados de forma nativa
Un procedimiento almacenado compilado de forma nativa debe tener Hola siguientes opciones en su cláusula T-SQL con:

* NATIVE_COMPILATION
* SCHEMABINDING: tablas de significado que Hola procedimiento almacenado no pueden tener sus definiciones de columna cambia de cualquier forma que afectaría al procedimiento almacenado de hello, a menos que se coloque el procedimiento almacenado de Hola.

Un módulo nativo debe usar un gran [bloque ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para la administración de transacciones. No hay ningún rol para una instrucción BEGIN TRANSACTION o ROLLBACK TRANSACTION explícita. Si el código detecta una infracción de una regla de negocios, puede finalizar el bloque atomic Hola con un [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrucción.

### <a name="typical-create-procedure-for-natively-compiled"></a>CREATE PROCEDURE típico para compilar de forma nativa
Hola T-SQL toocreate un procedimiento almacenado compilado de forma nativa suele ser similar toohello después de plantilla:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Para hello TRANSACTION_ISOLATION_LEVEL, instantánea es procedimiento más habitual de valor para hello compilado de forma nativa almacenado de Hola. Sin embargo, un subconjunto de Hola otros valores también se admiten:
  
  * REPEATABLE READ
  * SERIALIZABLE
* Hola valor de idioma debe estar presente en la vista de sys.languages Hola.

### <a name="how-toomigrate-a-stored-procedure"></a>¿Cómo toomigrate un procedimiento almacenado
pasos de migración de Hello son:

1. Obtener Hola CREATE PROCEDURE script toohello procedimiento almacenado interpretado normal.
2. Vuelva a escribir su plantilla anterior de encabezado toomatch Hola.
3. Determinar si el procedimiento de hello almacenado código T-SQL utiliza las características que no se admiten para los procedimientos almacenados compilados de forma nativa. Implemente soluciones alternativas si es necesario.
   
   * Para obtener información detallada, consulte [Problemas de migración para los procedimientos almacenados compilados de forma nativa](http://msdn.microsoft.com/library/dn296678.aspx).
4. Cambiar el nombre de procedimiento almacenado antiguo de hello mediante SP_RENAME. O bien, simplemente quítelo con la instrucción DROP.
5. Ejecute el script CREATE PROCEDURE T-SQL editado.

## <a name="step-6-run-your-workload-in-test"></a>Paso 6: Ejecutar la carga de trabajo en la prueba
Ejecutar una carga de trabajo en la base de datos de prueba de la carga de trabajo de toohello similares que se ejecuta en la base de datos de producción. Esto debería aclarar mejora del rendimiento Hola logrado mediante el uso de la característica de hello en memoria de tablas y procedimientos almacenados.

Los atributos principales de carga de trabajo de hello son:

* Número de conexiones simultáneas.
* Relación de lectura/escritura.

tootailor y carga de trabajo de prueba de ejecución hello, considere el uso de la herramienta de práctica ostress.exe hello, que se muestra en [aquí](sql-database-in-memory.md).

latencia de red toominimize, ejecute la prueba en hello misma región geográfica Azure donde existe la base de datos de Hola.

## <a name="step-7-post-implementation-monitoring"></a>Paso 7: Supervisión postimplementación
Considere la posibilidad de supervisar los efectos en el rendimiento de sus implementaciones en memoria en producción hello:

* [Supervisión del almacenamiento In-Memory](sql-database-in-memory-oltp-monitoring.md).
* [Supervisión de Base de datos SQL de Azure con vistas de administración dinámica](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Vínculos relacionados
* [In-Memory OLTP (optimización In-Memory)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Introducción tooNatively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn133184.aspx)
* [Asesor de optimización en memoria](http://msdn.microsoft.com/library/dn284308.aspx)

