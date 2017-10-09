---
title: "tooinstrument consultas en el almacén de datos de SQL de las etiquetas aaaUse | Documentos de Microsoft"
description: "Sugerencias para usar las consultas de tooinstrument de etiquetas en el almacén de datos de SQL Azure para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Usar consultas de tooinstrument de etiquetas en el almacén de datos de SQL
Almacenamiento de datos SQL admite un concepto conocido como etiquetas de consulta. Antes de entrar en materia, vamos a ver un ejemplo:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Esta última línea etiquetas consulta de hello cadena 'Mi consulta Label' toohello. Esto es particularmente útil como etiqueta de hello está capacitado para la consulta a través de hello DMV. Esto nos proporciona un tootrack mecanismo hacia abajo de consultas problemáticas y también toohelp identificar progreso a través de una ejecución ETL.

Una buena convención de nomenclatura realmente ayuda en este caso. Por ejemplo, algo como "proyecto: procedimiento: instrucción: comentario ' ayudaría a toouniquely identificar consultas de hello en entre todo el código de hello en control de código fuente.

Hola a toosearch por etiqueta puede usar Hola después de consulta que usa vistas de administración dinámica:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Es fundamental que ajuste corchetes o comillas dobles alrededor de la etiqueta de palabra Hola al realizar una consulta. Etiqueta es una palabra reservada y producirá un error si no se ha delimitado.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
