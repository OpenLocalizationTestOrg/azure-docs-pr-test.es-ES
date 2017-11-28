---
title: "nivel de compatibilidad del modelo de aaaData en los servicios de análisis de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="59e58-103">Nivel de compatibilidad para los modelos tabulares de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="59e58-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="59e58-104">*Nivel de compatibilidad* hace referencia a comportamientos específicos de toorelease en el motor de Analysis Services de Hola.</span><span class="sxs-lookup"><span data-stu-id="59e58-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="59e58-105">Nivel de compatibilidad de cambios toohello normalmente coincida con las versiones principales de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="59e58-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="59e58-106">Estos cambios también se implementan en paridad de toomaintain Azure Analysis Services entre ambas plataformas.</span><span class="sxs-lookup"><span data-stu-id="59e58-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="59e58-107">Los cambios de nivel de compatibilidad también afectan a las características disponibles en los modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="59e58-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="59e58-108">Por ejemplo, los metadatos de objetos tabulares y de DirectQuery tienen implementaciones diferentes según el nivel de compatibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="59e58-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="59e58-109">Azure Analysis Services es compatible con los modelos tabulares en niveles de compatibilidad de hello 1200 y 1400.</span><span class="sxs-lookup"><span data-stu-id="59e58-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="59e58-110">nivel de compatibilidad más reciente de Hello es 1400.</span><span class="sxs-lookup"><span data-stu-id="59e58-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="59e58-111">Este nivel se corresponde a SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="59e58-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="59e58-112">Principales características de nivel de compatibilidad de hello 1400 incluyen:</span><span class="sxs-lookup"><span data-stu-id="59e58-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="59e58-113">Nueva infraestructura para la conectividad de datos y la importación en los modelos tabulares con compatibilidad con las API de TOM y el scripting de TMSL.</span><span class="sxs-lookup"><span data-stu-id="59e58-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="59e58-114">Esta nueva característica habilita la compatibilidad con orígenes de datos adicionales como Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="59e58-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="59e58-115">Funcionalidades de transformación de datos y mashup de datos mediante el uso de expresiones Get Data y M.</span><span class="sxs-lookup"><span data-stu-id="59e58-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="59e58-116">Las medidas admiten una propiedad de filas de detalles con una expresión DAX.</span><span class="sxs-lookup"><span data-stu-id="59e58-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="59e58-117">Esta propiedad habilita las herramientas de cliente como Microsoft Excel toodrill toodetailed datos de un informe de agregado.</span><span class="sxs-lookup"><span data-stu-id="59e58-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="59e58-118">Por ejemplo, cuando los usuarios ver las ventas totales para una región y el mes, pueden ver detalles del pedido Hola asociado.</span><span class="sxs-lookup"><span data-stu-id="59e58-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="59e58-119">Seguridad de nivel de objeto de tabla y columna de nombres, además toohello datos dentro de ellos.</span><span class="sxs-lookup"><span data-stu-id="59e58-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="59e58-120">Compatibilidad mejorada para las jerarquías desiguales.</span><span class="sxs-lookup"><span data-stu-id="59e58-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="59e58-121">Mejoras en el rendimiento y la supervisión.</span><span class="sxs-lookup"><span data-stu-id="59e58-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="59e58-122">Establecimiento del nivel de compatibilidad</span><span class="sxs-lookup"><span data-stu-id="59e58-122">Set compatibility level</span></span> 
 <span data-ttu-id="59e58-123">Al crear un nuevo proyecto de modelo tabular en SSDT, puede especificar el nivel de compatibilidad de hello en hello **Diseñador de modelos tabulares** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="59e58-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="59e58-125">Si selecciona hello **no volver a mostrar este mensaje** opción, todos los proyectos posteriores utilizan nivel de compatibilidad de hello especificado como valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="59e58-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="59e58-126">Puede cambiar el nivel de compatibilidad de hello predeterminado en SSDT en **herramientas** > **opciones**.</span><span class="sxs-lookup"><span data-stu-id="59e58-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="59e58-127">tooupgrade un proyecto de modelo tabular existente en SSDT, conjunto hello **nivel de compatibilidad** propiedad en el modelo de hello **propiedades** ventana.</span><span class="sxs-lookup"><span data-stu-id="59e58-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="59e58-128">Tenga en cuenta que, actualizar el nivel de compatibilidad de hello es irreversible.</span><span class="sxs-lookup"><span data-stu-id="59e58-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="59e58-129">Compruebe el nivel de compatibilidad para una base de datos de modelo tabular en SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="59e58-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="59e58-130">En SSMS, haga clic en el nombre de base de datos de hello > **propiedades** > **nivel de compatibilidad**.</span><span class="sxs-lookup"><span data-stu-id="59e58-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="59e58-131">Comprobación del nivel de compatibilidad admitido para un servidor en SSMS</span><span class="sxs-lookup"><span data-stu-id="59e58-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="59e58-132">En SSMS, haga clic en el nombre del servidor de hello > **propiedades** > **nivel de compatibilidad admitido**.</span><span class="sxs-lookup"><span data-stu-id="59e58-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="59e58-133">Esta propiedad especifica Hola máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor de hello (excepto la vista previa).</span><span class="sxs-lookup"><span data-stu-id="59e58-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="59e58-134">no se puede cambiar el nivel de compatibilidad de Hello compatible.</span><span class="sxs-lookup"><span data-stu-id="59e58-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="59e58-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59e58-135">Next steps</span></span>
  <span data-ttu-id="59e58-136">[Creación de un modelo en Azure Portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="59e58-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="59e58-137">Administración de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="59e58-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
