---
title: "Implementación en Azure Analysis Services mediante SSDT | Microsoft Docs"
description: Aprenda a implementar un modelo tabular en un servidor de Azure Analysis Services mediante SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="61b66-103">Implementación de un modelo desde SSDT</span><span class="sxs-lookup"><span data-stu-id="61b66-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="61b66-104">Una vez que ha creado un servidor en su suscripción de Azure, está listo para implementar una base de datos de modelo tabular en él.</span><span class="sxs-lookup"><span data-stu-id="61b66-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="61b66-105">Puede utilizar SQL Server Data Tools (SSDT) para compilar e implementar un proyecto de modelo tabular que esté trabajando.</span><span class="sxs-lookup"><span data-stu-id="61b66-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="61b66-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="61b66-106">Prerequisites</span></span>
<span data-ttu-id="61b66-107">Para empezar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61b66-107">To get started, you need:</span></span>

* <span data-ttu-id="61b66-108">**Servidor de Analysis Services** en Azure.</span><span class="sxs-lookup"><span data-stu-id="61b66-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="61b66-109">Para más información, consulte [Creación de un servidor de Azure Analysis Services en Azure Portal](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="61b66-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="61b66-110">**Proyecto de modelo tabular** en SSDT o un modelo tabular existente en el nivel de compatibilidad 1200 o superior.</span><span class="sxs-lookup"><span data-stu-id="61b66-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="61b66-111">¿Nunca ha creado ninguno?</span><span class="sxs-lookup"><span data-stu-id="61b66-111">Never created one?</span></span> <span data-ttu-id="61b66-112">Pruebe el [tutorial de modelado tabular de ventas en Internet de Adventure Works](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="61b66-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="61b66-113">**Puerta de enlace local**: si uno o varios orígenes de datos son locales en la red de su organización, debe instalar una [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="61b66-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="61b66-114">La puerta de enlace es necesaria para que el servidor en la nube se conecte a sus orígenes de datos locales para procesar y actualizar los datos en el modelo.</span><span class="sxs-lookup"><span data-stu-id="61b66-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="61b66-115">Antes de implementarlo, asegúrese de que puede procesar los datos de las tablas.</span><span class="sxs-lookup"><span data-stu-id="61b66-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="61b66-116">En SSDT, haga clic en **Modelo** > **Proceso** > **Procesar todo**.</span><span class="sxs-lookup"><span data-stu-id="61b66-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="61b66-117">Si se produce un error de procesamiento, no se implementará correctamente.</span><span class="sxs-lookup"><span data-stu-id="61b66-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="61b66-118">Para implementar un modelo tabular desde SSDT</span><span class="sxs-lookup"><span data-stu-id="61b66-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="61b66-119">Antes de realizar la implementación, es preciso obtener el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="61b66-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="61b66-120">En **Azure Portal** > servidor > **Información general** > **Nombre de servidor**, copie el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="61b66-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="61b66-122">En SSDT > **Explorador de soluciones**, haga clic con el botón derecho en el proyecto > **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="61b66-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="61b66-123">A continuación, en **Implementación** > **Servidor**, pegue el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="61b66-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Pegar el nombre del servidor en la propiedad del servidor de implementación](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="61b66-125">En el **Explorador de soluciones**, haga clic con el botón derecho en **Propiedades** y haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="61b66-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="61b66-126">Es posible que se le pida que inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="61b66-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Implementación en el servidor](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="61b66-128">El estado de la implementación aparece en la ventana Salida y en Implementar.</span><span class="sxs-lookup"><span data-stu-id="61b66-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Estado de implementación](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="61b66-130">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="61b66-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="61b66-131">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="61b66-131">Troubleshooting</span></span>
<span data-ttu-id="61b66-132">Si se produce un error al implementar los metadatos, es probable que sea porque SSDT no se pudo conectar al servidor.</span><span class="sxs-lookup"><span data-stu-id="61b66-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="61b66-133">Asegúrese de poder conectarse al servidor mediante SSMS.</span><span class="sxs-lookup"><span data-stu-id="61b66-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="61b66-134">A continuación, asegúrese de que la propiedad de Servidor de implementación del proyecto es correcta.</span><span class="sxs-lookup"><span data-stu-id="61b66-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="61b66-135">Si se produce un error al realizar una implementación en una tabla, es probable que sea porque el servidor no pudo conectarse a un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="61b66-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="61b66-136">Si el origen de datos es local en la red de su organización, asegúrese de instalar una [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="61b66-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b66-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61b66-137">Next steps</span></span>
<span data-ttu-id="61b66-138">Ahora que tiene el modelo tabular implementado en el servidor, está listo para conectarse a él.</span><span class="sxs-lookup"><span data-stu-id="61b66-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="61b66-139">Puede [conectarse a él con SSMS](analysis-services-manage.md) para administrarlo.</span><span class="sxs-lookup"><span data-stu-id="61b66-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="61b66-140">Además, puede [conectarse a él mediante una herramienta cliente](analysis-services-connect.md) como Power BI, Power BI Desktop o Excel y empezar a crear informes.</span><span class="sxs-lookup"><span data-stu-id="61b66-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

