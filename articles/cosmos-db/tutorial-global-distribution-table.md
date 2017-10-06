---
title: "tutorial de distribución global de Cosmos DB aaaAzure de API de tabla | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla."
services: cosmos-db
keywords: "distribución global, Table"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de tabla

En este artículo, le mostramos cómo toouse Hola distribución global de base de datos de Azure Cosmos toosetup de portal de Azure y, a continuación, conectarse con hello API de tabla (vista previa).

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello [API de tabla](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Conexión tooa región preferida mediante Hola API de tabla

En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform. Esto puede hacerse por establecer hello `TablePreferredLocations` valor de configuración en la configuración de aplicación hello para la vista previa de hello SDK de almacenamiento de Azure. En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y ha especificado, la lista de preferencias Hola Hola mayoría extremo óptimo se elegirá por tooperform del SDK de almacenamiento de Azure de hello escribir y las operaciones de lectura.

Hola `TablePreferredLocations` debe contener una lista separada por comas de ubicaciones (hospedaje múltiple) preferidos para las lecturas. Cada instancia del cliente puede especificar un subconjunto de estas regiones en orden de hello preferido para las lecturas de latencia baja. regiones de Hello deben denominarse mediante sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`.

Todas las lecturas se enviarán toohello primera región disponible en hello `TablePreferredLocations` lista. Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente.

Hola SDK sólo intentará tooread de regiones de hello especificado en `TablePreferredLocations`. Por lo tanto, por ejemplo, si Hola cuenta de base de datos está disponible en tres regiones, pero solo para cliente hello especifica dos de Hola regiones de escritura para `TablePreferredLocations`, a continuación, no se enviará ningún lecturas fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.

Hola SDK enviará automáticamente todas las escrituras toohello actual escritura región.

Si hello `TablePreferredLocations` propiedad no está establecida, todas las solicitudes se servirá de región de escritura actual de Hola.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

De este modo finaliza este tutorial. Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md). Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello DocumentDB APIs

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.

> [!div class="nextstepaction"]
> [Desarrollar localmente con el emulador de Hola](local-emulator.md)
