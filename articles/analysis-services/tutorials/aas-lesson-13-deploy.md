---
title: "Lección 13 del tutorial de Analysis Services: Implementación | Microsoft Docs"
description: "Se describe cómo implementar el proyecto del tutorial en Azure Analysis Services."
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
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="5834f-103">Lección 13: Implementación</span><span class="sxs-lookup"><span data-stu-id="5834f-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="5834f-104">En esta lección, configurará propiedades de implementación. Para ello, especificará un servidor de Azure Analysis Services en el que realizar la implementación y un nombre para el modelo.</span><span class="sxs-lookup"><span data-stu-id="5834f-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="5834f-105">A continuación, implementará el modelo en esa instancia.</span><span class="sxs-lookup"><span data-stu-id="5834f-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="5834f-106">Después de implementa el modelo, los usuarios pueden conectarse a él mediante una aplicación cliente de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="5834f-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="5834f-107">Para más información, consulte [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) (Implementación en Azure Analysis Services).</span><span class="sxs-lookup"><span data-stu-id="5834f-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="5834f-108">Tiempo estimado para completar esta lección: **5 minutos**</span><span class="sxs-lookup"><span data-stu-id="5834f-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="5834f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5834f-109">Prerequisites</span></span>  
<span data-ttu-id="5834f-110">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="5834f-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="5834f-111">Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 12: Análisis en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="5834f-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="5834f-112">Debe tener [permisos de administrador](../analysis-services-server-admins.md) en el servidor remoto de Analysis Services para poder implementarla.</span><span class="sxs-lookup"><span data-stu-id="5834f-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="5834f-113">Si instaló la base de datos de ejemplo AdventureWorksDW2014 en un servidor local de SQL y va a implementar el modelo en un servidor de Azure Analysis Services, se requiere una [puerta de enlace de datos local](../analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="5834f-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="5834f-114">Implementación del modelo</span><span class="sxs-lookup"><span data-stu-id="5834f-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="5834f-115">Para configurar las propiedades de implementación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5834f-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="5834f-116">En **el Explorador de soluciones**, haga clic con el botón derecho en el proyecto **AW Internet Sales** y luego haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="5834f-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="5834f-117">En el cuadro de diálogo **AW Internet Sales Property Pages**, en **Servidor de implementación**, en la propiedad **Servidor**, escriba el nombre completo de un servidor.</span><span class="sxs-lookup"><span data-stu-id="5834f-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="5834f-119">En la propiedad **Base de datos**, escriba **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="5834f-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="5834f-120">En la propiedad **Nombre del modelo**, escriba **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="5834f-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="5834f-121">Compruebe sus selecciones y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5834f-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="5834f-122">Para implementar Adventure Works Internet Sales, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5834f-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="5834f-123">En el **Explorador de soluciones**, haga clic con el botón derecho en el **proyecto AW Internet Sales** > **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="5834f-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="5834f-124">Haga clic con el botón derecho en el **proyecto AW Internet Sales** > **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="5834f-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="5834f-125">Al realizar la implementación en Azure Analysis Services, puede que se le pida que escriba su contraseña.</span><span class="sxs-lookup"><span data-stu-id="5834f-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="5834f-126">Escriba su cuenta profesional y la contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe estar en Administradores en el servidor.</span><span class="sxs-lookup"><span data-stu-id="5834f-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="5834f-127">Aparece el cuadro de diálogo Implementar y muestra el estado de implementación de los metadatos y cada tabla incluida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="5834f-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="5834f-129">Cuando la implementación finalice correctamente, siga adelante y haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="5834f-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="5834f-130">Conclusión</span><span class="sxs-lookup"><span data-stu-id="5834f-130">Conclusion</span></span>  
<span data-ttu-id="5834f-131">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="5834f-131">Congratulations!</span></span> <span data-ttu-id="5834f-132">Ha terminado de crear e implementar el primer modelo tabular de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="5834f-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="5834f-133">Este tutorial le ha ayudado a completar las tareas más comunes en la creación de un modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="5834f-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="5834f-134">Ahora que el modelo Adventure Works Internet Sales está implementado, puede usar SQL Server Management Studio para administrarlo; cree scripts de proceso y un plan de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5834f-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="5834f-135">Ahora los usuarios pueden conectarse también al modelo mediante una aplicación cliente de generación de informes, como Microsoft Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="5834f-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="5834f-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5834f-137">What's next?</span></span>
<span data-ttu-id="5834f-138">[Conexión con Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="5834f-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="5834f-139">[Lección complementaria: Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="5834f-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="5834f-140">[Lección complementaria: Filas de detalles](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="5834f-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="5834f-141">Lección complementaria: Jerarquías desiguales</span><span class="sxs-lookup"><span data-stu-id="5834f-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
