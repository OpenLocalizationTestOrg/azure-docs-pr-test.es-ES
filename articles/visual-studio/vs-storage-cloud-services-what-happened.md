---
title: "¿Qué le ha ocurrido a mi proyecto de servicio en la nube? | Microsoft Docs"
description: "Describe lo que sucede en un proyecto de servicios en la nube después de conectarse a una cuenta de almacenamiento de Azure mediante los servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 4c9de56f6daf07097c0f593db37d14dce3bce05f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="5732f-104">¿Qué le ha ocurrido a mi proyecto de servicios en la nube (servicio conectado a Almacenamiento de Azure de Visual Studio)?</span><span class="sxs-lookup"><span data-stu-id="5732f-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="5732f-105">Se han agregado referencias</span><span class="sxs-lookup"><span data-stu-id="5732f-105">References added</span></span>
<span data-ttu-id="5732f-106">El paquete NuGet de Almacenamiento de Azure se agregó al proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5732f-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="5732f-107">Este paquete agrega las siguientes referencias. NET:</span><span class="sxs-lookup"><span data-stu-id="5732f-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="5732f-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5732f-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5732f-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5732f-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5732f-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5732f-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5732f-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="5732f-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="5732f-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="5732f-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="5732f-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="5732f-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="5732f-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="5732f-114">**System.Data**</span></span>
* <span data-ttu-id="5732f-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5732f-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="5732f-116">Se ha agregado la cadena de conexión para Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5732f-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="5732f-117">Se han creado elementos con la cadena y la clave de conexión de la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="5732f-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="5732f-118">Se han hecho modificaciones en los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5732f-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="5732f-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="5732f-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="5732f-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="5732f-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="5732f-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="5732f-121">**ServiceConfiguration.Local.cscfg**</span></span>

