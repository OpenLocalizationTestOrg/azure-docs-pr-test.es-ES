---
title: Lista de todos los trabajos de Azure Import/Export | Microsoft Docs
description: "Descubra cómo enumerar todos los trabajos del servicio Azure Import/Export de una suscripción."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="c1eba-103">Enumeración de los trabajos del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="c1eba-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="c1eba-104">Para enumerar todos los trabajos de una suscripción, llame a la operación [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) (Enumerar trabajos).</span><span class="sxs-lookup"><span data-stu-id="c1eba-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="c1eba-105">`List Jobs` devuelve una lista de trabajos, así como los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="c1eba-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="c1eba-106">El tipo de trabajo (importación o exportación)</span><span class="sxs-lookup"><span data-stu-id="c1eba-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="c1eba-107">El estado actual del trabajo</span><span class="sxs-lookup"><span data-stu-id="c1eba-107">The current job state</span></span>

-   <span data-ttu-id="c1eba-108">La cuenta de almacenamiento asociada al trabajo</span><span class="sxs-lookup"><span data-stu-id="c1eba-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1eba-109">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1eba-109">Next steps</span></span>

* [<span data-ttu-id="c1eba-110">Uso de la API de REST del servicio Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="c1eba-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
