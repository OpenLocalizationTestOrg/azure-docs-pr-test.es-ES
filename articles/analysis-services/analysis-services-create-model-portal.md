---
title: "aaaCreate un modelo tabular mediante el Diseñador de hello Web de servicios de análisis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un modelo tabular de Analysis Services de Azure mediante el uso de Hola Diseñador Web de portal de Azure."
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
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="abdb4-103">Creación de un modelo en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="abdb4-103">Create a model in Azure portal</span></span>

<span data-ttu-id="abdb4-104">característica del diseñador (versión preliminar) web Hello Azure Analysis Services en el portal de Azure proporciona una manera rápida y sencilla toocreate y editar los modelos tabulares y consulta del modelo datos directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="abdb4-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="abdb4-105">Tenga en cuenta, el diseñador web hello es **vista previa**.</span><span class="sxs-lookup"><span data-stu-id="abdb4-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="abdb4-106">Mientras se agrega nueva funcionalidad de todo el tiempo hello, en vista previa, la funcionalidad es limitada.</span><span class="sxs-lookup"><span data-stu-id="abdb4-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="abdb4-107">Para el desarrollo de modelos más avanzados y pruebas, es mejor toouse Visual Studio (SSDT) y SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="abdb4-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abdb4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abdb4-108">Prerequisites</span></span>

- <span data-ttu-id="abdb4-109">Un servidor de Analysis Services de Azure en nivel Standard o Developer de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdb4-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="abdb4-110">Nuevos modelos creados mediante el Diseñador de hello Web son DirectQuery, solo compatible con estos niveles.</span><span class="sxs-lookup"><span data-stu-id="abdb4-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="abdb4-111">Un archivo Power BI Desktop (.pbix), Azure SQL Database o Azure SQL Data Warehouse como origen de datos.</span><span class="sxs-lookup"><span data-stu-id="abdb4-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="abdb4-112">Los nuevos modelos creados a partir de archivos Power BI Desktop admiten orígenes de datos de Azure SQL Database, Azure SQL Data Warehouse, Oracle y Teradata.</span><span class="sxs-lookup"><span data-stu-id="abdb4-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="abdb4-113">Una cuenta de SQL Server y la contraseña para conectarse a orígenes de datos de base de datos SQL o almacenamiento de datos de SQL Azure tooAzure.</span><span class="sxs-lookup"><span data-stu-id="abdb4-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="abdb4-114">toocreate un nuevo modelo tabular</span><span class="sxs-lookup"><span data-stu-id="abdb4-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="abdb4-115">En la hoja del servidor **Introducción** >  **Web designer**, haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="abdb4-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Creación de un modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="abdb4-117">En **Web designer** > **Modelos**, haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="abdb4-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Creación de un modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="abdb4-119">En **Nuevo modelo**, escriba un nombre de modelo y, a continuación, seleccione un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="abdb4-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Cuadro de diálogo Nuevo modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="abdb4-121">En **conectar**, especifique las propiedades de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdb4-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="abdb4-122">El nombre de usuario y la contraseña deben ser de una cuenta de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="abdb4-122">Username and password must be a SQL Server account.</span></span>

     ![Cuadro de diálogo Connect (Conexión) en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="abdb4-124">En **tablas y vistas**, seleccionar hello tooinclude de tablas en el modelo y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="abdb4-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="abdb4-125">Se crean automáticamente relaciones entre las tablas con un par de claves.</span><span class="sxs-lookup"><span data-stu-id="abdb4-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selección de tablas y vistas](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="abdb4-127">El nuevo modelo aparece en el explorador.</span><span class="sxs-lookup"><span data-stu-id="abdb4-127">Your new model appears in your browser.</span></span> <span data-ttu-id="abdb4-128">Desde aquí puede:</span><span class="sxs-lookup"><span data-stu-id="abdb4-128">From here, you can:</span></span>   

- <span data-ttu-id="abdb4-129">Consultar datos del modelo arrastrando el Diseñador de consultas de campos toohello y agregando filtros.</span><span class="sxs-lookup"><span data-stu-id="abdb4-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="abdb4-130">Crear nuevas medidas en tablas.</span><span class="sxs-lookup"><span data-stu-id="abdb4-130">Create new measures in tables.</span></span>
- <span data-ttu-id="abdb4-131">Editar los metadatos del modelo mediante el editor de json de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdb4-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="abdb4-132">Abrir el modelo de hello en Visual Studio (SSDT), Power BI Desktop o Excel.</span><span class="sxs-lookup"><span data-stu-id="abdb4-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selección de tablas y vistas](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="abdb4-134">Al editar los metadatos del modelo o crear nuevas medidas en el explorador, está guardando los modelos de tooyour cambios en Azure.</span><span class="sxs-lookup"><span data-stu-id="abdb4-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="abdb4-135">Si también está trabajando en el modelo en SSDT, Power BI Desktop o Excel, el modelo puede dejar de estar sincronizado.</span><span class="sxs-lookup"><span data-stu-id="abdb4-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="abdb4-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abdb4-136">Next steps</span></span> 
[<span data-ttu-id="abdb4-137">Administración de usuarios y roles de base de datos</span><span class="sxs-lookup"><span data-stu-id="abdb4-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="abdb4-138">Conexión con Excel</span><span class="sxs-lookup"><span data-stu-id="abdb4-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


