---
title: Bibliotecas de cliente necesarias para conectarse a Azure Analysis Services | Microsoft Docs
description: Se describen las bibliotecas de cliente necesarias para que las aplicaciones cliente y las herramientas de cliente se conecten a Azure Analysis Services.
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="f6e9b-103">Bibliotecas de cliente para la conexión a Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="f6e9b-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="f6e9b-104">Se requieren bibliotecas de cliente para que las aplicaciones cliente y las herramientas de cliente se puedan conectar a servidores de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="f6e9b-105">Analysis Services usa tres bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="f6e9b-106">ADOMD.NET y los objetos de administración de Analysis Services (AMO), son bibliotecas de cliente administradas.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="f6e9b-107">El proveedor OLE DB de Analysis Services (MSOLAP DLL) es una biblioteca de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="f6e9b-108">Normalmente, las tres bibliotecas se instalan al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="f6e9b-109">Azure Analysis Services requiere la versión más reciente de las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="f6e9b-110">Las aplicaciones cliente de Microsoft, como Power BI Desktop y Excel, instalan las tres bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="f6e9b-111">Sin embargo, dependiendo de la versión o la frecuencia de las actualizaciones, las bibliotecas de cliente pueden no ser las versiones más recientes que necesita Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="f6e9b-112">Esto mismo se aplica a aplicaciones personalizadas u otras interfaces, como AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="f6e9b-113">Estas aplicaciones requieren la instalación manual de las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="f6e9b-114">Las bibliotecas de cliente para la instalación manual se incluyen en los paquetes de características de SQL Server como paquetes de distribución.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="f6e9b-115">Sin embargo, estas bibliotecas de cliente están asociadas a la versión de SQL Server y no pueden ser la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="f6e9b-116">Las bibliotecas de cliente para conexiones de cliente son diferentes de los proveedores de datos necesarios para conectarse desde un servidor de Azure Analysis Services a un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="f6e9b-117">Para más información sobre las conexiones de origen de datos, consulte [Conexiones a origen de datos](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="f6e9b-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="f6e9b-118">Descargar las bibliotecas de cliente más recientes</span><span class="sxs-lookup"><span data-stu-id="f6e9b-118">Download the latest client libraries</span></span>  
<span data-ttu-id="f6e9b-119">Use las siguientes bibliotecas de cliente si se encuentra en un entorno de producción y necesita versiones totalmente finales y que ofrezcan una compatibilidad plena.</span><span class="sxs-lookup"><span data-stu-id="f6e9b-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="f6e9b-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="f6e9b-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="f6e9b-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="f6e9b-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="f6e9b-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="f6e9b-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="f6e9b-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="f6e9b-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="f6e9b-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6e9b-124">Next steps</span></span>
<span data-ttu-id="f6e9b-125">[Connect with Excel](analysis-services-connect-excel.md)   (Conexión con Excel)</span><span class="sxs-lookup"><span data-stu-id="f6e9b-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="f6e9b-126">Conexión con Power BI</span><span class="sxs-lookup"><span data-stu-id="f6e9b-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
