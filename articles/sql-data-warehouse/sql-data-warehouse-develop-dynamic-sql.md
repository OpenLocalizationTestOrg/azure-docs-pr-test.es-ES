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
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="6be13-103">SQL dinámico en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="6be13-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="6be13-104">Al desarrollar el código de la aplicación para almacenamiento de datos de SQL, es posible que necesita toouse sql dinámico toohelp entregar soluciones flexibles, genéricas y modulares.</span><span class="sxs-lookup"><span data-stu-id="6be13-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="6be13-105">Almacenamiento de datos SQL no admite por el momento tipos de datos blob.</span><span class="sxs-lookup"><span data-stu-id="6be13-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="6be13-106">Esto puede limitar el tamaño de Hola de las cadenas como tipos de blob incluyen tipos varchar (max) y nvarchar (max).</span><span class="sxs-lookup"><span data-stu-id="6be13-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="6be13-107">Si ha usado estos tipos en el código de aplicación al generar cadenas muy grandes, necesitará toobreak Hola código en fragmentos y use Hola EXEC instrucción en su lugar.</span><span class="sxs-lookup"><span data-stu-id="6be13-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="6be13-108">Un ejemplo sencillo:</span><span class="sxs-lookup"><span data-stu-id="6be13-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="6be13-109">Si la cadena hello es corta puede usar [sp_executesql] [ sp_executesql] con normalidad.</span><span class="sxs-lookup"><span data-stu-id="6be13-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="6be13-110">Las instrucciones ejecutadas como SQL dinámico se seguirán las reglas de validación de asunto tooall TSQL.</span><span class="sxs-lookup"><span data-stu-id="6be13-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6be13-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6be13-111">Next steps</span></span>
<span data-ttu-id="6be13-112">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="6be13-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
