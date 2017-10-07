---
title: el archivo de datos de aaaLoad desde archivo CSV en base de datos de SQL de Azure (copia masiva bcp) | Documentos de Microsoft
description: "Para un tamaño de datos pequeños, utiliza datos de tooimport de bcp en la base de datos de SQL Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="4ff43-103">Carga de datos desde CSV en Azure SQL Database (archivos planos)</span><span class="sxs-lookup"><span data-stu-id="4ff43-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="4ff43-104">Puede usar datos de tooimport de utilidad de línea de comandos de hello bcp desde un archivo CSV en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4ff43-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ff43-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4ff43-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="4ff43-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ff43-106">Prerequisites</span></span>
<span data-ttu-id="4ff43-107">Hola toocomplete los pasos de este artículo, es necesario:</span><span class="sxs-lookup"><span data-stu-id="4ff43-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="4ff43-108">Un servidor lógico de Base de datos SQL de Azure y una base de datos</span><span class="sxs-lookup"><span data-stu-id="4ff43-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="4ff43-109">utilidad de línea de comandos de Hello bcp instalado</span><span class="sxs-lookup"><span data-stu-id="4ff43-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="4ff43-110">utilidad de línea de comandos de sqlcmd Hola instalada</span><span class="sxs-lookup"><span data-stu-id="4ff43-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="4ff43-111">Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="4ff43-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="4ff43-112">Datos en los formatos ASCII o UTF-16</span><span class="sxs-lookup"><span data-stu-id="4ff43-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="4ff43-113">Si está tratando de este tutorial con sus propios datos, necesita los datos toouse Hola ASCII o la codificación UTF-16 dado bcp no es compatible con UTF-8.</span><span class="sxs-lookup"><span data-stu-id="4ff43-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="4ff43-114">1. Creación de una tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="4ff43-114">1. Create a destination table</span></span>
<span data-ttu-id="4ff43-115">Definir una tabla de base de datos de SQL como tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ff43-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="4ff43-116">columnas de Hello en la tabla de hello deben corresponder toohello datos en cada fila de su archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="4ff43-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="4ff43-117">toocreate una tabla, abra un símbolo del sistema y use sqlcmd.exe toorun Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4ff43-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="4ff43-118">2. Creación de un archivo de datos de origen</span><span class="sxs-lookup"><span data-stu-id="4ff43-118">2. Create a source data file</span></span>
<span data-ttu-id="4ff43-119">Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="4ff43-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="4ff43-120">Estos datos están en formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="4ff43-120">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="4ff43-121">(Opcional) tooexport sus propios datos de una base de datos de SQL Server, abra un símbolo del sistema y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ff43-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="4ff43-122">Reemplace TableName, ServerName, DatabaseName, Username y Password por su propia información.</span><span class="sxs-lookup"><span data-stu-id="4ff43-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="4ff43-123">3. Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="4ff43-123">3. Load hello data</span></span>
<span data-ttu-id="4ff43-124">datos de hello tooload, abra un símbolo del sistema y ejecute hello siguiente comando, reemplazando los valores de hello para nombre del servidor, nombre de base de datos, nombre de usuario y contraseña con su propia información.</span><span class="sxs-lookup"><span data-stu-id="4ff43-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="4ff43-125">Utilice este comando tooverify hello se cargaron correctamente los datos</span><span class="sxs-lookup"><span data-stu-id="4ff43-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="4ff43-126">resultados de Hello deberían tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4ff43-126">hello results should look like this:</span></span>

| <span data-ttu-id="4ff43-127">DateId</span><span class="sxs-lookup"><span data-stu-id="4ff43-127">DateId</span></span> | <span data-ttu-id="4ff43-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4ff43-128">CalendarQuarter</span></span> | <span data-ttu-id="4ff43-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4ff43-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ff43-130">20150101</span><span class="sxs-lookup"><span data-stu-id="4ff43-130">20150101</span></span> |<span data-ttu-id="4ff43-131">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-131">1</span></span> |<span data-ttu-id="4ff43-132">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-132">3</span></span> |
| <span data-ttu-id="4ff43-133">20150201</span><span class="sxs-lookup"><span data-stu-id="4ff43-133">20150201</span></span> |<span data-ttu-id="4ff43-134">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-134">1</span></span> |<span data-ttu-id="4ff43-135">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-135">3</span></span> |
| <span data-ttu-id="4ff43-136">20150301</span><span class="sxs-lookup"><span data-stu-id="4ff43-136">20150301</span></span> |<span data-ttu-id="4ff43-137">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-137">1</span></span> |<span data-ttu-id="4ff43-138">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-138">3</span></span> |
| <span data-ttu-id="4ff43-139">20150401</span><span class="sxs-lookup"><span data-stu-id="4ff43-139">20150401</span></span> |<span data-ttu-id="4ff43-140">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-140">2</span></span> |<span data-ttu-id="4ff43-141">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-141">4</span></span> |
| <span data-ttu-id="4ff43-142">20150501</span><span class="sxs-lookup"><span data-stu-id="4ff43-142">20150501</span></span> |<span data-ttu-id="4ff43-143">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-143">2</span></span> |<span data-ttu-id="4ff43-144">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-144">4</span></span> |
| <span data-ttu-id="4ff43-145">20150601</span><span class="sxs-lookup"><span data-stu-id="4ff43-145">20150601</span></span> |<span data-ttu-id="4ff43-146">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-146">2</span></span> |<span data-ttu-id="4ff43-147">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-147">4</span></span> |
| <span data-ttu-id="4ff43-148">20150701</span><span class="sxs-lookup"><span data-stu-id="4ff43-148">20150701</span></span> |<span data-ttu-id="4ff43-149">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-149">3</span></span> |<span data-ttu-id="4ff43-150">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-150">1</span></span> |
| <span data-ttu-id="4ff43-151">20150801</span><span class="sxs-lookup"><span data-stu-id="4ff43-151">20150801</span></span> |<span data-ttu-id="4ff43-152">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-152">3</span></span> |<span data-ttu-id="4ff43-153">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-153">1</span></span> |
| <span data-ttu-id="4ff43-154">20150801</span><span class="sxs-lookup"><span data-stu-id="4ff43-154">20150801</span></span> |<span data-ttu-id="4ff43-155">3</span><span class="sxs-lookup"><span data-stu-id="4ff43-155">3</span></span> |<span data-ttu-id="4ff43-156">1</span><span class="sxs-lookup"><span data-stu-id="4ff43-156">1</span></span> |
| <span data-ttu-id="4ff43-157">20151001</span><span class="sxs-lookup"><span data-stu-id="4ff43-157">20151001</span></span> |<span data-ttu-id="4ff43-158">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-158">4</span></span> |<span data-ttu-id="4ff43-159">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-159">2</span></span> |
| <span data-ttu-id="4ff43-160">20151101</span><span class="sxs-lookup"><span data-stu-id="4ff43-160">20151101</span></span> |<span data-ttu-id="4ff43-161">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-161">4</span></span> |<span data-ttu-id="4ff43-162">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-162">2</span></span> |
| <span data-ttu-id="4ff43-163">20151201</span><span class="sxs-lookup"><span data-stu-id="4ff43-163">20151201</span></span> |<span data-ttu-id="4ff43-164">4</span><span class="sxs-lookup"><span data-stu-id="4ff43-164">4</span></span> |<span data-ttu-id="4ff43-165">2</span><span class="sxs-lookup"><span data-stu-id="4ff43-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ff43-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ff43-166">Next steps</span></span>
<span data-ttu-id="4ff43-167">toomigrate una base de datos de SQL Server, vea [migración de base de datos de SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="4ff43-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
