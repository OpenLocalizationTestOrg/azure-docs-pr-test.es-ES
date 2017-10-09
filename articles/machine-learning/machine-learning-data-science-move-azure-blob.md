---
title: aaaMove tooand de datos desde el almacenamiento de blobs de Azure | Documentos de Microsoft
description: Mover datos tooand desde el almacenamiento de blobs de Azure
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
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="99de0-103">Mover datos tooand desde el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="99de0-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="99de0-104">El método más adecuado para usted dependerá de su escenario.</span><span class="sxs-lookup"><span data-stu-id="99de0-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="99de0-105">Hola [escenarios para análisis avanzado en aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md) artículo le ayuda a determinar los recursos de Hola que necesita para una variedad de flujos de trabajo de ciencia de datos usados en hello avanzada de proceso de análisis.</span><span class="sxs-lookup"><span data-stu-id="99de0-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="99de0-106">Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="99de0-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="99de0-107">Como alternativa, puede usar [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) para:</span><span class="sxs-lookup"><span data-stu-id="99de0-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="99de0-108">crear y programar una canalización que descarga los datos desde Azure Blob Storage,</span><span class="sxs-lookup"><span data-stu-id="99de0-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="99de0-109">pasarlo tooa publica el servicio web de aprendizaje automático de Azure,</span><span class="sxs-lookup"><span data-stu-id="99de0-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="99de0-110">recibir los resultados de análisis predictivos de hello, y</span><span class="sxs-lookup"><span data-stu-id="99de0-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="99de0-111">cargar Hola resultados toostorage.</span><span class="sxs-lookup"><span data-stu-id="99de0-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="99de0-112">Consulte [Creación de canalizaciones predictivas mediante Factoría de datos de Azure y Aprendizaje automático de Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md)para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="99de0-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99de0-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99de0-113">Prerequisites</span></span>
<span data-ttu-id="99de0-114">Este documento se da por supuesto que tiene una suscripción de Azure, una cuenta de almacenamiento y la clave de almacenamiento correspondiente de Hola para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="99de0-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="99de0-115">Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="99de0-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="99de0-116">tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99de0-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="99de0-117">Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="99de0-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

