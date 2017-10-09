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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="b3089-103">Usar consultas de tooinstrument de etiquetas en el almacén de datos de SQL</span><span class="sxs-lookup"><span data-stu-id="b3089-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="b3089-104">Almacenamiento de datos SQL admite un concepto conocido como etiquetas de consulta.</span><span class="sxs-lookup"><span data-stu-id="b3089-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="b3089-105">Antes de entrar en materia, vamos a ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b3089-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="b3089-106">Esta última línea etiquetas consulta de hello cadena 'Mi consulta Label' toohello.</span><span class="sxs-lookup"><span data-stu-id="b3089-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="b3089-107">Esto es particularmente útil como etiqueta de hello está capacitado para la consulta a través de hello DMV.</span><span class="sxs-lookup"><span data-stu-id="b3089-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="b3089-108">Esto nos proporciona un tootrack mecanismo hacia abajo de consultas problemáticas y también toohelp identificar progreso a través de una ejecución ETL.</span><span class="sxs-lookup"><span data-stu-id="b3089-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="b3089-109">Una buena convención de nomenclatura realmente ayuda en este caso.</span><span class="sxs-lookup"><span data-stu-id="b3089-109">A good naming convention really helps here.</span></span> <span data-ttu-id="b3089-110">Por ejemplo, algo como "proyecto: procedimiento: instrucción: comentario ' ayudaría a toouniquely identificar consultas de hello en entre todo el código de hello en control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="b3089-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="b3089-111">Hola a toosearch por etiqueta puede usar Hola después de consulta que usa vistas de administración dinámica:</span><span class="sxs-lookup"><span data-stu-id="b3089-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="b3089-112">Es fundamental que ajuste corchetes o comillas dobles alrededor de la etiqueta de palabra Hola al realizar una consulta.</span><span class="sxs-lookup"><span data-stu-id="b3089-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="b3089-113">Etiqueta es una palabra reservada y producirá un error si no se ha delimitado.</span><span class="sxs-lookup"><span data-stu-id="b3089-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b3089-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3089-114">Next steps</span></span>
<span data-ttu-id="b3089-115">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="b3089-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
