---
title: Uso de etiquetas para instrumentar consultas en SQL Data Warehouse | Microsoft Docs
description: Sugerencias para usar etiquetas para instrumentar las consultas en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
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
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="ecc79-103">Uso de etiquetas para instrumentar consultas en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ecc79-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="ecc79-104">Almacenamiento de datos SQL admite un concepto conocido como etiquetas de consulta.</span><span class="sxs-lookup"><span data-stu-id="ecc79-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="ecc79-105">Antes de entrar en materia, vamos a ver un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecc79-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="ecc79-106">Esta última línea etiqueta la cadena 'Mi etiqueta de consulta' a la consulta.</span><span class="sxs-lookup"><span data-stu-id="ecc79-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="ecc79-107">Esto es especialmente útil dado que la etiqueta se puede consultar a través de las DMV.</span><span class="sxs-lookup"><span data-stu-id="ecc79-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="ecc79-108">De esta manera contamos con un mecanismo para realizar el seguimiento de los problemas y también para ayudar a identificar el progreso a través de una ejecución de ETL.</span><span class="sxs-lookup"><span data-stu-id="ecc79-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="ecc79-109">Una buena convención de nomenclatura realmente ayuda en este caso.</span><span class="sxs-lookup"><span data-stu-id="ecc79-109">A good naming convention really helps here.</span></span> <span data-ttu-id="ecc79-110">Por ejemplo, algo como ' PROYECTO : PROCEDIMIENTO : INSTRUCCIÓN : COMENTARIO' ayudaría a identificar de forma única la consulta entre todo el código de control del código fuente.</span><span class="sxs-lookup"><span data-stu-id="ecc79-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="ecc79-111">Para buscar por etiqueta, puede usar la siguiente consulta que emplea las vistas de administración dinámica:</span><span class="sxs-lookup"><span data-stu-id="ecc79-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="ecc79-112">Es esencial que encierre entre corchetes o comillas dobles la etiqueta de la palabra al consultar.</span><span class="sxs-lookup"><span data-stu-id="ecc79-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="ecc79-113">Etiqueta es una palabra reservada y producirá un error si no se ha delimitado.</span><span class="sxs-lookup"><span data-stu-id="ecc79-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ecc79-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecc79-114">Next steps</span></span>
<span data-ttu-id="ecc79-115">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="ecc79-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
