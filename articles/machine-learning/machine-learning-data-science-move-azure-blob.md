---
title: Mover datos hacia y desde Azure Blob Storage | Microsoft Docs
description: Mover datos hacia y desde el almacenamiento de blobs de Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="09f4e-103">Movimiento de datos hacia y desde Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="09f4e-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="09f4e-104">El método más adecuado para usted dependerá de su escenario.</span><span class="sxs-lookup"><span data-stu-id="09f4e-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="09f4e-105">El artículo [Escenarios para análisis avanzado en Aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md) lo ayudará a determinar los recursos que necesita para una variedad de flujos de trabajo de ciencia de datos utilizados en el proceso de análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="09f4e-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="09f4e-106">Para ver una introducción completa a Azure Blob Storage, consulte [Aspectos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="09f4e-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="09f4e-107">Como alternativa, puede usar [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) para:</span><span class="sxs-lookup"><span data-stu-id="09f4e-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="09f4e-108">crear y programar una canalización que descarga los datos desde Azure Blob Storage,</span><span class="sxs-lookup"><span data-stu-id="09f4e-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="09f4e-109">pasarla a un servicio web Azure Machine Learning publicado,</span><span class="sxs-lookup"><span data-stu-id="09f4e-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="09f4e-110">recibir los resultados de análisis predictivo y</span><span class="sxs-lookup"><span data-stu-id="09f4e-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="09f4e-111">cargar los resultados al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09f4e-111">upload the results to storage.</span></span> 

<span data-ttu-id="09f4e-112">Consulte [Creación de canalizaciones predictivas mediante Factoría de datos de Azure y Aprendizaje automático de Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="09f4e-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09f4e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09f4e-113">Prerequisites</span></span>
<span data-ttu-id="09f4e-114">En este documento se supone que tiene una suscripción de Azure y una cuenta de almacenamiento y la clave de almacenamiento correspondiente para dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="09f4e-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="09f4e-115">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="09f4e-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="09f4e-116">Para configurar una suscripción a Azure, consulte [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09f4e-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="09f4e-117">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="09f4e-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

