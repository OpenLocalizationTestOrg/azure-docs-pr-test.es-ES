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
# <a name="move-data-tooand-from-azure-blob-storage"></a>Mover datos tooand desde el almacenamiento de blobs de Azure
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

El método más adecuado para usted dependerá de su escenario. Hola [escenarios para análisis avanzado en aprendizaje automático de Azure](machine-learning-data-science-plan-sample-scenarios.md) artículo le ayuda a determinar los recursos de Hola que necesita para una variedad de flujos de trabajo de ciencia de datos usados en hello avanzada de proceso de análisis.

> [!NOTE]
> Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

Como alternativa, puede usar [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) para: 

* crear y programar una canalización que descarga los datos desde Azure Blob Storage, 
* pasarlo tooa publica el servicio web de aprendizaje automático de Azure, 
* recibir los resultados de análisis predictivos de hello, y 
* cargar Hola resultados toostorage. 

Consulte [Creación de canalizaciones predictivas mediante Factoría de datos de Azure y Aprendizaje automático de Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md)para obtener más información.

## <a name="prerequisites"></a>Requisitos previos
Este documento se da por supuesto que tiene una suscripción de Azure, una cuenta de almacenamiento y la clave de almacenamiento correspondiente de Hola para esa cuenta. Antes de cargar o descargar datos, debe conocer su nombre de cuenta de almacenamiento de Azure y la clave de cuenta.

* tooset una suscripción de Azure, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener instrucciones sobre la creación de una cuenta de almacenamiento y para obtener información de cuentas y claves, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

