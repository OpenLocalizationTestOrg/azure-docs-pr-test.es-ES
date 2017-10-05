---
title: Uso de Azure Data Factory con SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 7cd113f4a92635bc68253c2beb165ad1f0c96569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="b5aa3-103">Uso de Factoría de datos de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b5aa3-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="b5aa3-104">Factoría de datos de Azure ofrece un método completamente administrado para organizar la transferencia de datos y la ejecución de los procedimientos almacenados en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b5aa3-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="b5aa3-105">Esto le permitirá configurar y programar con mayor facilidad los complejos procedimientos de extracción, transformación y carga (ETL) con Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b5aa3-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="b5aa3-106">Para obtener una introducción más completa de Azure Data Factory, consulte [Documentación de Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="b5aa3-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="b5aa3-107">Movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="b5aa3-107">Data Movement</span></span>
<span data-ttu-id="b5aa3-108">Factoría de datos de Azure permite el movimiento entre orígenes locales y los distintos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5aa3-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="b5aa3-109">En general, la integración actual con Factoría de datos de Azure es compatible con el movimiento de datos desde y hacia las ubicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="b5aa3-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="b5aa3-110">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="b5aa3-110">Azure blob storage</span></span>
* <span data-ttu-id="b5aa3-111">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="b5aa3-111">Azure SQL Database</span></span>
* <span data-ttu-id="b5aa3-112">SQL Server local</span><span class="sxs-lookup"><span data-stu-id="b5aa3-112">On-premises SQL Server</span></span>
* <span data-ttu-id="b5aa3-113">SQL Server en IaaS</span><span class="sxs-lookup"><span data-stu-id="b5aa3-113">SQL Server on IaaS</span></span>

<span data-ttu-id="b5aa3-114">Para obtener información sobre cómo configurar una actividad de copia de datos, consulte [Copia de datos con Azure Data Factory][Copy data with Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="b5aa3-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="b5aa3-115">Procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="b5aa3-115">Stored Procedures</span></span>
 <span data-ttu-id="b5aa3-116">De la misma manera en que se puede programar la transferencia de datos, Factoría de datos de Azure también se puede usar para organizar la ejecución de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="b5aa3-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="b5aa3-117">Esto permite que se creen canalizaciones más complejas y extiende la capacidad de Factoría de datos de Azure para aprovechar la potencia de cálculo de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="b5aa3-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5aa3-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5aa3-118">Next steps</span></span>
<span data-ttu-id="b5aa3-119">Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="b5aa3-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="b5aa3-120">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="b5aa3-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

