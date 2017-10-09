---
title: "aaaDynamic SQL en el almacén de datos de SQL | Documentos de Microsoft"
description: "Sugerencias para usar SQL dinámico en Almacenamiento de datos SQL Azure para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>SQL dinámico en Almacenamiento de datos SQL
Al desarrollar el código de la aplicación para almacenamiento de datos de SQL, es posible que necesita toouse sql dinámico toohelp entregar soluciones flexibles, genéricas y modulares. Almacenamiento de datos SQL no admite por el momento tipos de datos blob. Esto puede limitar el tamaño de Hola de las cadenas como tipos de blob incluyen tipos varchar (max) y nvarchar (max). Si ha usado estos tipos en el código de aplicación al generar cadenas muy grandes, necesitará toobreak Hola código en fragmentos y use Hola EXEC instrucción en su lugar.

Un ejemplo sencillo:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Si la cadena hello es corta puede usar [sp_executesql] [ sp_executesql] con normalidad.

> [!NOTE]
> Las instrucciones ejecutadas como SQL dinámico se seguirán las reglas de validación de asunto tooall TSQL.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
