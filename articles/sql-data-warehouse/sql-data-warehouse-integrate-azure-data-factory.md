---
title: aaaUse Data Factory de Azure con almacenamiento de datos SQL | Documentos de Microsoft
description: "Sugerencias para usar Factoría de datos de Azure (ADF) con Almacenamiento de datos SQL para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="00486-103">Uso de Factoría de datos de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="00486-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="00486-104">Factoría de datos de Azure proporciona un método completamente administrado para orquestar la transferencia de Hola de datos y la ejecución de procedimientos almacenados de almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="00486-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="00486-105">Esto le permitirá toomore fácilmente instalación y programación extraer transformación y carga (ETL) procedimientos complejos con almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="00486-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="00486-106">Para obtener una descripción más completa de Data Factory de Azure, vea hello [documentación de Data Factory de Azure][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="00486-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="00486-107">Movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="00486-107">Data Movement</span></span>
<span data-ttu-id="00486-108">Factoría de datos de Azure permite el movimiento entre orígenes locales y los distintos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="00486-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="00486-109">Integración general y actual con Data Factory de Azure admite tooand de movimiento de datos de hello ubicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="00486-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="00486-110">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="00486-110">Azure blob storage</span></span>
* <span data-ttu-id="00486-111">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="00486-111">Azure SQL Database</span></span>
* <span data-ttu-id="00486-112">SQL Server local</span><span class="sxs-lookup"><span data-stu-id="00486-112">On-premises SQL Server</span></span>
* <span data-ttu-id="00486-113">SQL Server en IaaS</span><span class="sxs-lookup"><span data-stu-id="00486-113">SQL Server on IaaS</span></span>

<span data-ttu-id="00486-114">Para obtener información sobre cómo tooset los datos de una actividad de copia [copiar los datos con Data Factory de Azure][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="00486-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="00486-115">Procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="00486-115">Stored Procedures</span></span>
 <span data-ttu-id="00486-116">Hola igual forma se puede utilizar tooschedule la transferencia de datos, puede Data Factory de Azure también puede tooorchestrate usado Hola ejecución de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="00486-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="00486-117">Esto permite más compleja toobe canalizaciones creado y extiende capacidad tooleverage Hola potencia de cálculo del generador de datos de Azure de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="00486-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00486-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00486-118">Next steps</span></span>
<span data-ttu-id="00486-119">Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="00486-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="00486-120">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="00486-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

