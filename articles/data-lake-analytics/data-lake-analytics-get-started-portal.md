---
title: "aaaGet iniciado con análisis de Data Lake de Azure mediante el portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo crear un trabajo de análisis de Data Lake mediante SQL U toouse hello toocreate portal Azure una cuenta de análisis de Data Lake y enviar el trabajo de Hola. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="d9679-103">Introducción al uso de Azure Portal por parte de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d9679-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="d9679-104">Obtenga información acerca de cómo toouse Hola cuentas de análisis de Azure Data Lake de Azure toocreate portal, definir trabajos en [U-SQL](data-lake-analytics-u-sql-get-started.md)y enviar el servicio de análisis de Data Lake toohello de trabajos.</span><span class="sxs-lookup"><span data-stu-id="d9679-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="d9679-105">Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9679-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9679-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d9679-106">Prerequisites</span></span>

<span data-ttu-id="d9679-107">Para comenzar este tutorial, es preciso tener una **suscripción a Azure**.</span><span class="sxs-lookup"><span data-stu-id="d9679-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="d9679-108">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9679-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="d9679-109">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="d9679-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="d9679-110">Ahora, se creará un análisis de Data Lake y un almacén de Data Lake cuenta Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="d9679-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="d9679-111">Este paso es sencillo y sólo tarda aproximadamente toofinish de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="d9679-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="d9679-112">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9679-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d9679-113">Haga clic en **Nuevo** >  **Datos y análisis** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d9679-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="d9679-114">Seleccione los valores de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d9679-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="d9679-115">**Nombre**: nombre de la cuenta de Data Lake Analytics (solo se permiten letras minúsculas y números).</span><span class="sxs-lookup"><span data-stu-id="d9679-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="d9679-116">**Suscripción**: elija la suscripción de Azure usada para la cuenta de análisis de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d9679-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="d9679-117">**Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d9679-117">**Resource Group**.</span></span> <span data-ttu-id="d9679-118">seleccione un grupo de recursos de Azure existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d9679-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="d9679-119">**Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="d9679-119">**Location**.</span></span> <span data-ttu-id="d9679-120">Seleccione un centro de datos de Azure para la cuenta de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="d9679-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="d9679-121">**Almacén de Data Lake**: siga Hola instrucción toocreate una nueva cuenta de almacén de Data Lake o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="d9679-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="d9679-122">Si lo desea, seleccione un plan de tarifa para la cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d9679-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="d9679-123">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d9679-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="d9679-124">El primer script U-SQL</span><span class="sxs-lookup"><span data-stu-id="d9679-124">Your first U-SQL script</span></span>

<span data-ttu-id="d9679-125">Hola después de texto es un script U-SQL muy simple.</span><span class="sxs-lookup"><span data-stu-id="d9679-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="d9679-126">Todo lo que hace es definir un conjunto de datos pequeño script de Hola y, a continuación, escriba ese conjunto de datos a almacén de Data Lake de toohello de forma predeterminada como un archivo denominado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="d9679-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="d9679-127">Envío de un trabajo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="d9679-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="d9679-128">En la cuenta de análisis de Data Lake hello, haga clic en **nuevo trabajo**.</span><span class="sxs-lookup"><span data-stu-id="d9679-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="d9679-129">Pegue en texto hello de hello script U-SQL mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d9679-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="d9679-130">Haga clic en **Enviar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="d9679-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="d9679-131">Espere hasta que cambie de estado de trabajo de hello demasiado**correcto**.</span><span class="sxs-lookup"><span data-stu-id="d9679-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="d9679-132">Si se produce un error en el trabajo de hello, consulte [supervisar y solucionar problemas de trabajos de análisis de Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d9679-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="d9679-133">Haga clic en hello **salida** ficha y, a continuación, haga clic en `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="d9679-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="d9679-134">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d9679-134">See also</span></span>

* <span data-ttu-id="d9679-135">tooget a desarrollar aplicaciones SQL U, consulte [scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9679-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="d9679-136">toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9679-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="d9679-137">Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9679-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
