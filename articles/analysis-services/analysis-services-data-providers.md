---
title: bibliotecas de aaaClient necesarias para conectar tooAzure Analysis Services | Documentos de Microsoft
description: Describe las bibliotecas de cliente necesarias para las aplicaciones y herramientas de cliente, tooconnect Azure Analysis Services
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="0e395-103">Bibliotecas de cliente para conectar tooAzure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0e395-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="0e395-104">Bibliotecas de cliente son necesarias para las aplicaciones cliente y servidores de servicios de herramientas tooconnect tooAnalysis.</span><span class="sxs-lookup"><span data-stu-id="0e395-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="0e395-105">Analysis Services usa tres bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="0e395-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="0e395-106">ADOMD.NET y los objetos de administración de Analysis Services (AMO), son bibliotecas de cliente administradas.</span><span class="sxs-lookup"><span data-stu-id="0e395-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="0e395-107">proveedor de OLE DB de Analysis Services de Hello (MSOLAP DLL) es una biblioteca de cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="0e395-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="0e395-108">Normalmente, las tres se instalan en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0e395-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="0e395-109">Azure Analysis Services requiere que las versiones más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e395-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="0e395-110">Las aplicaciones cliente de Microsoft, como Power BI Desktop y Excel, instalan las tres bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="0e395-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="0e395-111">Sin embargo, dependiendo de la versión de Hola o la frecuencia de las actualizaciones, las bibliotecas de cliente no pueden ser versiones más recientes de hello requeridas por los servicios de análisis de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e395-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="0e395-112">Hello mismo aplica toocustom aplicaciones u otras interfaces, como AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="0e395-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="0e395-113">Estas aplicaciones requieren la instalación manual de las bibliotecas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e395-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="0e395-114">bibliotecas de cliente de Hello para la instalación manual se incluyen en los paquetes de características de SQL Server como paquetes de distribución.</span><span class="sxs-lookup"><span data-stu-id="0e395-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="0e395-115">Sin embargo, estas bibliotecas de cliente son de la versión de SQL Server toohello relacionados y no pueden ser hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="0e395-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="0e395-116">Bibliotecas de cliente para conexiones de cliente son diferentes de tooconnect necesaria de proveedores de datos de un origen de datos de Azure Analysis Services server tooa.</span><span class="sxs-lookup"><span data-stu-id="0e395-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="0e395-117">toolearn más información acerca de las conexiones de origen de datos, vea [las conexiones de origen de datos](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="0e395-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="0e395-118">Descargar las bibliotecas de cliente más recientes de Hola</span><span class="sxs-lookup"><span data-stu-id="0e395-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="0e395-119">Usar hello siguiendo las bibliotecas de cliente si se encuentra en un entorno de producción y necesita las versiones de lanzamiento y soporte completos.</span><span class="sxs-lookup"><span data-stu-id="0e395-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="0e395-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="0e395-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="0e395-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="0e395-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="0e395-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="0e395-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="0e395-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="0e395-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="0e395-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e395-124">Next steps</span></span>
<span data-ttu-id="0e395-125">[Connect with Excel](analysis-services-connect-excel.md)   (Conexión con Excel)</span><span class="sxs-lookup"><span data-stu-id="0e395-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="0e395-126">Conexión con Power BI</span><span class="sxs-lookup"><span data-stu-id="0e395-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
