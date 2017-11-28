---
title: aaaDeploy tooAzure Analysis Services mediante el uso de SSDT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy un tooan de modelo tabular Azure Analysis Services server mediante el uso de SSDT."
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="22637-103">Implementación de un modelo desde SSDT</span><span class="sxs-lookup"><span data-stu-id="22637-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="22637-104">Una vez que ha creado un servidor en su suscripción de Azure, está listo toodeploy un tooit de base de datos de modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="22637-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="22637-105">Puede usar SQL Server Data Tools (SSDT) toobuild e implementar un proyecto de modelo tabular que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="22637-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="22637-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22637-106">Prerequisites</span></span>
<span data-ttu-id="22637-107">tooget iniciado, debe:</span><span class="sxs-lookup"><span data-stu-id="22637-107">tooget started, you need:</span></span>

* <span data-ttu-id="22637-108">**Servidor de Analysis Services** en Azure.</span><span class="sxs-lookup"><span data-stu-id="22637-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="22637-109">más información, consulte toolearn [crear un servidor de Analysis Services de Azure](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="22637-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="22637-110">**Proyecto de modelos tabulares** en SSDT o un modelo tabular existente en Hola 1200 o nivel de compatibilidad superior.</span><span class="sxs-lookup"><span data-stu-id="22637-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="22637-111">¿Nunca ha creado ninguno?</span><span class="sxs-lookup"><span data-stu-id="22637-111">Never created one?</span></span> <span data-ttu-id="22637-112">Intente hello [tutorial de modelado tabular ventas de Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="22637-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="22637-113">**Puerta de enlace local** -si uno o varios orígenes de datos de forma local en la red de su organización, es necesario tooinstall una [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="22637-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="22637-114">puerta de enlace de Hello es necesario para la conexión de su servidor en la nube de hello tooyour datos orígenes tooprocess y la actualización de datos locales en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="22637-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="22637-115">Antes de implementar, asegúrese de que puede procesar los datos de hello en las tablas.</span><span class="sxs-lookup"><span data-stu-id="22637-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="22637-116">En SSDT, haga clic en **Modelo** > **Proceso** > **Procesar todo**.</span><span class="sxs-lookup"><span data-stu-id="22637-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="22637-117">Si se produce un error de procesamiento, no se implementará correctamente.</span><span class="sxs-lookup"><span data-stu-id="22637-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="22637-118">toodeploy un modelo tabular desde SSDT</span><span class="sxs-lookup"><span data-stu-id="22637-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="22637-119">Antes de implementar, necesita el nombre del servidor de tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="22637-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="22637-120">En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, el nombre del servidor de copia Hola.</span><span class="sxs-lookup"><span data-stu-id="22637-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="22637-122">En SSDT > **el Explorador de soluciones**, proyecto de hello contextual > **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="22637-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="22637-123">A continuación, en **implementación** > **Server** pegar el nombre del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="22637-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Pegar el nombre del servidor en la propiedad del servidor de implementación](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="22637-125">En el **Explorador de soluciones**, haga clic con el botón derecho en **Propiedades** y haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="22637-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="22637-126">Es posible que toosign solicitada en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="22637-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Implementar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="22637-128">Estado de la implementación aparece en ventana de salida Hola y de implementar.</span><span class="sxs-lookup"><span data-stu-id="22637-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Estado de implementación](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="22637-130">Eso es todo lo hay tooit!</span><span class="sxs-lookup"><span data-stu-id="22637-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="22637-131">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="22637-131">Troubleshooting</span></span>
<span data-ttu-id="22637-132">Si se produce un error en la implementación al implementar metadatos, es probable porque SSDT no pudo conectar a servidor tooyour.</span><span class="sxs-lookup"><span data-stu-id="22637-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="22637-133">Asegúrese de que se puede conectar servidor tooyour con SSMS.</span><span class="sxs-lookup"><span data-stu-id="22637-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="22637-134">A continuación, asegúrese de hello propiedad del servidor de implementación para el proyecto de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="22637-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="22637-135">Si se produce un error en la implementación en una tabla, es probable porque el servidor no pudo conectar el origen de datos de tooa.</span><span class="sxs-lookup"><span data-stu-id="22637-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="22637-136">Si el origen de datos es local en la red de su organización, que seguro tooinstall una [puerta de enlace de datos local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="22637-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="22637-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22637-137">Next steps</span></span>
<span data-ttu-id="22637-138">Ahora que tiene el servidor de modelo tabular implementado tooyour, está listo tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="22637-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="22637-139">También puede [conectar tooit con SSMS](analysis-services-manage.md) toomanage lo.</span><span class="sxs-lookup"><span data-stu-id="22637-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="22637-140">Además, puede [conectar tooit mediante una herramienta cliente](analysis-services-connect.md) como Power BI, Power BI Desktop o Excel y empezar a crear informes.</span><span class="sxs-lookup"><span data-stu-id="22637-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

