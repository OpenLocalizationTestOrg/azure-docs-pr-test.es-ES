---
title: "¿Qué le ha ocurrido a mi proyecto ASP.NET 5 (servicios conectados a Visual Studio)? | Microsoft Docs"
description: "Describe lo que sucede después de conectarse a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET 5 de Visual Studio mediante los servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2a25c24fd7625374d269622a805f386fcd52bb5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="b7547-103">¿Qué le ha ocurrido a mi proyecto ASP.NET 5 (servicios conectados a Almacenamiento de Azure de Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="b7547-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="b7547-104">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="b7547-104">References added</span></span>
<span data-ttu-id="b7547-105">El paquete NuGet de Almacenamiento de Azure se agregó al proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7547-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="b7547-106">Este paquete agrega las siguientes referencias. NET:</span><span class="sxs-lookup"><span data-stu-id="b7547-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="b7547-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="b7547-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="b7547-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="b7547-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="b7547-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="b7547-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="b7547-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="b7547-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="b7547-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="b7547-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="b7547-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="b7547-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="b7547-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="b7547-113">**System.Data**</span></span>
* <span data-ttu-id="b7547-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="b7547-114">**System.Spatial**</span></span>

<span data-ttu-id="b7547-115">Además, se agregó el paquete NuGet **Microsoft.Framework.Configuration.Json** .</span><span class="sxs-lookup"><span data-stu-id="b7547-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="b7547-116">Se ha agregado la cadena de conexión para Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7547-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="b7547-117">En el archivo config.json de su proyecto, se ha creado un elemento con la cadena y la clave de conexión de la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b7547-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="b7547-118">Para más información, vea [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="b7547-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

