---
title: aaaCreate granjas de servidores de SharePoint en Azure | Documentos de Microsoft
description: "Cree rápidamente una nueva granja de SharePoint 2013 o SharePoint 2016 en Azure con hello Azure marketplace portal."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="8e730-103">Crear conjuntos de servidores de SharePoint mediante hello Azure marketplace de portal</span><span class="sxs-lookup"><span data-stu-id="8e730-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="8e730-104">Granjas de servidores de SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8e730-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="8e730-105">Con el marketplace de portal de Microsoft Azure hello, puede crear rápidamente las granjas de servidores de SharePoint Server 2013 preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="8e730-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="8e730-106">Esto puede suponer un importante ahorro de tiempo si necesita una granja de SharePoint básica o de alta disponibilidad para un entorno de desarrollo y pruebas, o si va a evaluar SharePoint Server 2013 como solución de colaboración para su organización.</span><span class="sxs-lookup"><span data-stu-id="8e730-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="8e730-107">Hola **granja de servidores de SharePoint** se ha quitado el elemento de hello Azure Marketplace de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e730-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="8e730-108">Se ha reemplazado con hello **no - HA de granja de SharePoint 2013** y **granja de servidores de SharePoint 2013 HA** elementos.</span><span class="sxs-lookup"><span data-stu-id="8e730-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="8e730-109">granja de SharePoint básica de Hello consta de tres máquinas virtuales de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="8e730-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="8e730-111">Utilice esta configuración de granja simplificada para el desarrollo de aplicaciones de SharePoint en su primera evaluación de SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="8e730-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="8e730-112">granja de SharePoint de (tres servidores) básica de toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="8e730-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="8e730-113">Haga clic [aquí](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="8e730-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="8e730-114">Haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="8e730-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="8e730-115">En hello **no - HA de granja de SharePoint 2013** panel, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8e730-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="8e730-116">Especificar la configuración en los pasos de Hola de hello **crear no - HA de granja de SharePoint 2013** panel y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8e730-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="8e730-117">granja de SharePoint de alta disponibilidad de Hello consta de nueve máquinas virtuales en esta configuración.</span><span class="sxs-lookup"><span data-stu-id="8e730-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="8e730-119">Puede usar esta granja configuración tootest superior cargas máximas del cliente, alta disponibilidad Hola externo del sitio de SharePoint y los grupos de disponibilidad AlwaysOn de SQL Server para una granja de servidores de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e730-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="8e730-120">También puede usar esta configuración para el desarrollo de aplicaciones de SharePoint en un entorno de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="8e730-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="8e730-121">granja de SharePoint de toocreate Hola alta disponibilidad (servidor de nueve):</span><span class="sxs-lookup"><span data-stu-id="8e730-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="8e730-122">Haga clic [aquí](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="8e730-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="8e730-123">Haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="8e730-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="8e730-124">En hello **granja de servidores de SharePoint 2013 HA** panel, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8e730-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="8e730-125">Especificar la configuración en los pasos de hello siete de hello **crear HA de granja de SharePoint 2013** panel y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="8e730-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="8e730-126">No se puede crear hello **no - HA de granja de SharePoint 2013** o **granja de servidores de SharePoint 2013 HA** con una prueba gratuita de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e730-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="8e730-127">Hola portal de Azure crea dos de estos conjuntos de servidores en una red virtual solo en la nube con una presencia en web a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="8e730-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="8e730-128">No hay ningún sitio a sitio VPN o ExpressRoute conexión back-tooyour red la organización.</span><span class="sxs-lookup"><span data-stu-id="8e730-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="8e730-129">Cuando se crea hello básico o granjas de SharePoint de alta disponibilidad mediante Hola portal de Azure, no se puede especificar un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="8e730-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="8e730-130">toowork solucionar esta limitación, cree estas granjas de servidores con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e730-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="8e730-131">Para más información, vea [Crear granjas de servidores de desarrollo y pruebas de SharePoint 2013 con Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="8e730-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="8e730-132">Granjas de servidores de SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="8e730-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="8e730-133">Vea [este artículo](https://technet.microsoft.com/library/mt723354.aspx) para Hola Hola de toobuild instrucciones siguientes solo servidor SharePoint Server 2016 de la granja.</span><span class="sxs-lookup"><span data-stu-id="8e730-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="8e730-135">Administración de granjas de servidores de SharePoint de Hola</span><span class="sxs-lookup"><span data-stu-id="8e730-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="8e730-136">Puede administrar servidores de Hola de estos conjuntos de servidores a través de conexiones de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="8e730-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="8e730-137">Para obtener más información, consulte [inicie sesión en la máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="8e730-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="8e730-138">De sitio de SharePoint de Administración Central de hello, puede configurar Mis sitios, aplicaciones de SharePoint y otras funciones.</span><span class="sxs-lookup"><span data-stu-id="8e730-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="8e730-139">Para obtener más información, consulte [Configuración de SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e730-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e730-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e730-140">Next steps</span></span>
* <span data-ttu-id="8e730-141">Descubra más configuraciones de [SharePoint](https://technet.microsoft.com/library/dn635309.aspx) en los servicios de infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e730-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
