---
title: Nivel de compatibilidad del modelo de datos en Azure Analysis Services | Microsoft Docs
description: "Descripción del nivel de compatibilidad del modelo de datos tabulares."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: b11ba54c2cdc2675ec535368e7076613a5290212
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="7ce8e-103">Nivel de compatibilidad para los modelos tabulares de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7ce8e-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="7ce8e-104">El *nivel de compatibilidad* hace referencia a los comportamientos específicos de la versión del motor de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span></span> <span data-ttu-id="7ce8e-105">Normalmente, los cambios en el nivel de compatibilidad coinciden con las versiones principales de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="7ce8e-106">Estos cambios también se implementan en Azure Analysis Services para mantener la paridad entre ambas plataformas.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span></span> <span data-ttu-id="7ce8e-107">Los cambios de nivel de compatibilidad también afectan a las características disponibles en los modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="7ce8e-108">Por ejemplo, DirectQuery y los metadatos de objetos tabulares tienen implementaciones diferentes según el nivel de compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span></span> 

<span data-ttu-id="7ce8e-109">Azure Analysis Services admite modelos tabulares en los niveles de compatibilidad 1200 y 1400.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-109">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="7ce8e-110">El nivel de compatibilidad más reciente es el 1400.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-110">The latest compatibility level is 1400.</span></span> <span data-ttu-id="7ce8e-111">Este nivel se corresponde a SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="7ce8e-112">Entre las características principales del nivel de compatibilidad 1400 cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="7ce8e-112">Major features in the 1400 compatibility level include:</span></span>

*  <span data-ttu-id="7ce8e-113">Nueva infraestructura para la conectividad de datos y la importación en los modelos tabulares con compatibilidad con las API de TOM y el scripting de TMSL.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="7ce8e-114">Esta nueva característica habilita la compatibilidad con orígenes de datos adicionales como Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="7ce8e-115">Funcionalidades de transformación de datos y mashup de datos mediante el uso de expresiones Get Data y M.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="7ce8e-116">Las medidas admiten una propiedad de filas de detalles con una expresión DAX.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="7ce8e-117">Esta propiedad habilita herramientas de cliente como Microsoft Excel para profundizar en los datos detallados de un informe agregado.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-117">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span></span> <span data-ttu-id="7ce8e-118">Por ejemplo, cuando los usuarios ven las ventas totales para una región y mes, pueden ver los detalles del pedido asociados.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-118">For example, when users view total sales for a region and month, they can view the associated order details.</span></span> 
*  <span data-ttu-id="7ce8e-119">Seguridad en el nivel de objeto para los nombres de tablas y columnas, además de para los datos dentro de ellas.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-119">Object-level security for table and column names, in addition to the data within them.</span></span>
*  <span data-ttu-id="7ce8e-120">Compatibilidad mejorada para las jerarquías desiguales.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="7ce8e-121">Mejoras en el rendimiento y la supervisión.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="7ce8e-122">Establecimiento del nivel de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="7ce8e-122">Set compatibility level</span></span> 
 <span data-ttu-id="7ce8e-123">Al crear un nuevo proyecto de modelo tabular en SSDT, puede especificar el nivel de compatibilidad en el cuadro de diálogo **Diseñador de modelos tabulares**.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-123">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="7ce8e-125">Si selecciona la opción **No mostrar de nuevo este mensaje**, todos los proyectos posteriores usarán el nivel de compatibilidad que especificó como valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-125">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span></span> <span data-ttu-id="7ce8e-126">Puede cambiar el nivel de compatibilidad predeterminado en SSDT en **Herramientas** > **Opciones**.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-126">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="7ce8e-127">Para actualizar un proyecto de modelo tabular existente en SSDT, establezca la propiedad **Compatibility Level** en la ventana de **propiedades** del modelo.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-127">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span></span> <span data-ttu-id="7ce8e-128">Tenga en cuenta que la actualización del nivel de compatibilidad es irreversible.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-128">Keep in-mind, upgrading the compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="7ce8e-129">Compruebe el nivel de compatibilidad para una base de datos de modelo tabular en SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="7ce8e-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="7ce8e-130">En SSMS, haga clic con el botón derecho en el nombre de la base de datos > **Propiedades** > **Nivel de compatibilidad**.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-130">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="7ce8e-131">Comprobación del nivel de compatibilidad admitido para un servidor en SSMS</span><span class="sxs-lookup"><span data-stu-id="7ce8e-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="7ce8e-132">En SSMS, haga clic con el botón derecho en el nombre del servidor > **Propiedades** > **Nivel de compatibilidad admitido**.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-132">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="7ce8e-133">Esta propiedad especifica el máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor (excepto la versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="7ce8e-133">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span></span> <span data-ttu-id="7ce8e-134">El nivel de compatibilidad admitido no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="7ce8e-134">The supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7ce8e-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ce8e-135">Next steps</span></span>
  <span data-ttu-id="7ce8e-136">[Creación de un modelo en Azure Portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="7ce8e-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="7ce8e-137">Administración de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7ce8e-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
