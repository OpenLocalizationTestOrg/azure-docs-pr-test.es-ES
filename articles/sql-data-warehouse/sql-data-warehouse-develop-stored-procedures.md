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
# <a name="stored-procedures-in-sql-data-warehouse"></a>Procedimientos almacenados en el Almacenamiento de datos SQL
Almacenamiento de datos SQL es compatible con muchas características de Transact-SQL de Hola que se encuentran en SQL Server. Lo más importante es que hay características específicas que deseamos rendimiento de hello tooleverage toomaximize de la solución de escalado horizontal.

Sin embargo, escala de hello toomaintain y el rendimiento de almacenamiento de datos SQL no existe también son algunas de las características y funcionalidad que tienen diferencias de comportamiento y otros que no son compatibles.

Este artículo explica cómo tooimplement almacenan los procedimientos de almacenamiento de datos SQL.

## <a name="introducing-stored-procedures"></a>Introducción a los procedimientos almacenados
Los procedimientos almacenados son una excelente manera de encapsular el código SQL; almacenarlos tooyour cerrar datos en almacenamiento de datos de Hola. Encapsular el código de hello en unidades administrables procedimientos almacenados ayudan a los desarrolladores modularizar sus soluciones; facilitación de mayor reutilización del código. Cada procedimiento almacenado puede aceptar parámetros toomake ellos incluso más flexible.

El Almacenamiento de datos SQL proporciona una implementación optimizada y simplificada de procedimientos almacenados. Hola mayor diferencia en comparación con tooSQL Server es que Hola procedimiento almacenado no es código previamente compilado. En los almacenes de datos nos interesan generalmente menos con el tiempo de compilación de Hola. Es más importante que el código del procedimiento almacenado de hello correctamente está optimizado cuando se trabaja con grandes volúmenes de datos. objetivo de Hello es toosave horas, minutos y segundos no milisegundos. Por lo tanto, es más útil toothink de procedimientos almacenados como contenedores para la lógica SQL.     

Cuando se ejecuta el almacén de datos SQL las instrucciones de procedimiento almacenado Hola SQL son analizar, se traducen y optimizadas en tiempo de ejecución. Durante este proceso, cada instrucción se convierte en consultas distribuidas. Hola código SQL que se ejecuta realmente en datos de hello es consulta toohello diferentes enviada.

## <a name="nesting-stored-procedures"></a>Anidamiento de los procedimientos almacenados
Cuando los procedimientos almacenados llamar a otros procedimientos almacenados o ejecutar sql dinámico, a continuación, interna de hello del procedimiento almacenado o la invocación de código se dice que toobe anidados.

El Almacenamiento de datos SQL admite un máximo de ocho niveles de anidamiento. Esto es ligeramente diferente tooSQL Server. nivel de anidamiento de Hello en SQL Server es 32.

llamada de procedimiento almacenado de nivel superior de Hello equivale toonest nivel 1

```sql
EXEC prc_nesting
```
Si almacena Hola procedimiento también realiza EXEC otra llamada, a continuación, Esto aumentará too2 de nivel de anidamiento de Hola

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Si el segundo procedimiento de hello, a continuación, ejecuta algunos sql dinámico, a continuación, Esto aumentará too3 de nivel de anidamiento de Hola

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Tenga en cuenta que SQL Data Warehouse no admite actualmente @@NESTLEVEL. Deberá tookeep un seguimiento de su nivel de anidamiento usted mismo. No es probable alcanzará el límite de niveles de anidamiento de hello 8, pero si lo hace, necesitará toore-trabajo del código y "acoplarla" para que quepa dentro de este límite.

## <a name="insertexecute"></a>INSERT..EXECUTE
Almacenamiento de datos SQL no le permiten conjunto de resultados de hello tooconsume de un procedimiento almacenado con una instrucción INSERT. Sin embargo, puede utilizar un método alternativo.

Consulte toohello siguiente artículo de [tablas temporales] para obtener un ejemplo sobre cómo toodo esto.

## <a name="limitations"></a>Limitaciones
Existen algunos aspectos de los procedimientos almacenados de Transact-SQL que no se implementan en el Almacenamiento de datos SQL.

Son las siguientes:

* Procedimientos almacenados temporales
* Procedimientos almacenados numerados
* Procedimientos almacenados extendidos
* Procedimientos almacenados CLR
* Opción de cifrado
* Opción de replicación
* Parámetros con valores de tabla
* Parámetros de solo lectura
* Parámetros predeterminados
* Contextos de ejecución
* Instrucción de devolución

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[tablas temporales]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
