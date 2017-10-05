---
title: "Lección 12 del tutorial de Azure Analysis Services: Analizar en Excel | Microsoft Docs"
description: "Describe cómo usar Analizar en Excel en el proyecto del tutorial de Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="a3207-103">Lección 12: Analizar en Excel</span><span class="sxs-lookup"><span data-stu-id="a3207-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a3207-104">En esta lección se usa la característica Analizar en Excel para abrir Microsoft Excel, crear automáticamente una conexión con el área de trabajo del modelo y agregar automáticamente una tabla dinámica a la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="a3207-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="a3207-105">La característica Analizar en Excel está pensada para proporcionar una manera rápida y sencilla de probar la eficacia del diseño del modelo antes de implementarlo.</span><span class="sxs-lookup"><span data-stu-id="a3207-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="a3207-106">En esta lección no se realizan análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="a3207-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="a3207-107">El propósito de esta lección es conseguir que se familiarice, como autor del modelo, con las herramientas que puede usar para probar el diseño del modelo.</span><span class="sxs-lookup"><span data-stu-id="a3207-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="a3207-108">Para completar esta lección, debe tener Excel instalado en el mismo equipo que SSDT.</span><span class="sxs-lookup"><span data-stu-id="a3207-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="a3207-109">Tiempo estimado para completar esta lección: **cinco minutos**</span><span class="sxs-lookup"><span data-stu-id="a3207-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a3207-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3207-110">Prerequisites</span></span>  
<span data-ttu-id="a3207-111">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="a3207-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a3207-112">Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 11: Creación de roles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a3207-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="a3207-113">Examinar mediante las perspectivas predeterminada y Venta por Internet</span><span class="sxs-lookup"><span data-stu-id="a3207-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="a3207-114">En estas primeras tareas, examinará el modelo mediante la perspectiva predeterminada, que incluye todos los objetos del modelo, y mediante la perspectiva Venta por Internet.</span><span class="sxs-lookup"><span data-stu-id="a3207-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="a3207-115">La perspectiva Venta por Internet no incluye el objeto de tabla de clientes.</span><span class="sxs-lookup"><span data-stu-id="a3207-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="a3207-116">Para examinar mediante la perspectiva predeterminada</span><span class="sxs-lookup"><span data-stu-id="a3207-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="a3207-117">Haga clic en el menú **Modelo** > **Analizar en Excel**.</span><span class="sxs-lookup"><span data-stu-id="a3207-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="a3207-118">En el cuadro de diálogo **Analizar en Excel**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3207-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="a3207-119">Excel se abre con un nuevo libro.</span><span class="sxs-lookup"><span data-stu-id="a3207-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="a3207-120">Se crea una conexión de origen de datos con la cuenta de usuario actual y se usa la perspectiva predeterminada para definir los campos visibles.</span><span class="sxs-lookup"><span data-stu-id="a3207-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="a3207-121">Se agrega automáticamente una tabla dinámica a la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="a3207-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="a3207-122">En Excel, en la **Lista de campos de tabla dinámica**, observe que aparecen los grupos de medida **DimDate** y **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="a3207-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="a3207-123">También aparecen las tablas **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** y **FactInternetSales** con sus respectivas columnas.</span><span class="sxs-lookup"><span data-stu-id="a3207-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="a3207-124">Cierre Excel sin guardar el libro.</span><span class="sxs-lookup"><span data-stu-id="a3207-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="a3207-125">Para examinar mediante la perspectiva Venta por Internet</span><span class="sxs-lookup"><span data-stu-id="a3207-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="a3207-126">Haga clic en el menú **Modelo** y en **Analizar en Excel**.</span><span class="sxs-lookup"><span data-stu-id="a3207-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="a3207-127">En el cuadro de diálogo **Analizar en Excel**, deje seleccionado **Usuario de Windows actual**. Después, en el cuadro de lista desplegable **Perspectiva**, seleccione **Venta por Internet** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3207-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="a3207-129">En Excel, en **Campos de tabla dinámica**, observe que la tabla DimCustomer no está incluida en la lista de campos.</span><span class="sxs-lookup"><span data-stu-id="a3207-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="a3207-131">Cierre Excel sin guardar el libro.</span><span class="sxs-lookup"><span data-stu-id="a3207-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="a3207-132">Examinar mediante roles</span><span class="sxs-lookup"><span data-stu-id="a3207-132">Browse by using roles</span></span>  
<span data-ttu-id="a3207-133">Los roles son una parte importante de los modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="a3207-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="a3207-134">Si no hay al menos un rol al que agregar a los usuarios como miembros, los usuarios no pueden acceder a los datos del modelo ni analizarlos.</span><span class="sxs-lookup"><span data-stu-id="a3207-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="a3207-135">La característica Analizar en Excel le permite probar los roles que ha definido.</span><span class="sxs-lookup"><span data-stu-id="a3207-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="a3207-136">Para examinar mediante el rol de usuario Director de ventas</span><span class="sxs-lookup"><span data-stu-id="a3207-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="a3207-137">En SSDT, haga clic en el menú **Modelo** y en **Analizar en Excel**.</span><span class="sxs-lookup"><span data-stu-id="a3207-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="a3207-138">En **Especifique el nombre de usuario o rol que se va a usar al conectarse al modelo**, seleccione **Rol**. Después, en el cuadro de lista desplegable, seleccione **Jefe de ventas** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3207-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="a3207-139">Excel se abre con un nuevo libro.</span><span class="sxs-lookup"><span data-stu-id="a3207-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="a3207-140">Automáticamente se crea una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="a3207-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="a3207-141">En la lista de campos de tabla dinámica se incluyen todos los campos de datos disponibles en el nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="a3207-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="a3207-142">Cierre Excel sin guardar el libro.</span><span class="sxs-lookup"><span data-stu-id="a3207-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="a3207-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3207-143">What's next?</span></span>
<span data-ttu-id="a3207-144">Vaya a la siguiente lección: [Lección 13: Implementación](../tutorials/aas-lesson-13-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a3207-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
