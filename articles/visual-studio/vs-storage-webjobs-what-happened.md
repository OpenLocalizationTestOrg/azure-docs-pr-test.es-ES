---
title: "¿Qué le ha ocurrido a mi proyecto WebJob (servicio conectado a Almacenamiento de Azure de Visual Studio)? | Microsoft Docs"
description: "Describe lo que ha ocurrido en un proyecto WebJob de Azure después de conectarse a una cuenta de almacenamiento de Azure mediante los servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8891685a99c5ba366b74af0a21396d4a5e499835
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="c1268-104">¿Qué le ha ocurrido a mi proyecto WebJob (servicio conectado a Almacenamiento de Azure de Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="c1268-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="c1268-105">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="c1268-105">References Added</span></span>
<span data-ttu-id="c1268-106">El paquete de NuGet de Almacenamiento de Azure se agregó al proyecto de Visual Studio o se actualizó en él.</span><span class="sxs-lookup"><span data-stu-id="c1268-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="c1268-107">Este paquete agrega las siguientes referencias. NET:</span><span class="sxs-lookup"><span data-stu-id="c1268-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="c1268-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c1268-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c1268-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c1268-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c1268-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c1268-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c1268-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c1268-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="c1268-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="c1268-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="c1268-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="c1268-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="c1268-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="c1268-114">**System.Data**</span></span>
* <span data-ttu-id="c1268-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c1268-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="c1268-116">Se ha agregado la cadena de conexión para Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1268-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="c1268-117">En el archivo App.config del proyecto, se actualizaron las entradas **AzureWebJobsStorage** y **AzureWebJobsDashboard** con la cadena y la clave de conexión de la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c1268-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="c1268-118">Para obtener más información, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c1268-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

