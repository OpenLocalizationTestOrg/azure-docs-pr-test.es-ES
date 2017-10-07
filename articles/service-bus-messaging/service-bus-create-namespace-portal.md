---
title: aaaHow toocreate un espacio de nombres de Bus de servicio en hello portal de Azure | Documentos de Microsoft
description: Crear un espacio de nombres de Bus de servicio mediante Hola portal de Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Crear un espacio de nombres de Bus de servicio mediante Hola portal de Azure

Un espacio de nombres es un contenedor con un ámbito para todos los componentes de la mensajería. Varias colas y temas pueden residir en un único espacio de nombres, y los espacios de nombres suelen servir de contenedores de aplicación. Hay dos maneras diferentes toocreate un espacio de nombres de Bus de servicio:

1. Azure Portal (este artículo)
2. [Plantillas de Resource Manager][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Crear un espacio de nombres en hello portal de Azure

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

¡Enhorabuena! Ha creado un espacio de nombres de mensajería de Service Bus.

## <a name="next-steps"></a>Pasos siguientes

Visite nuestro [ejemplos de GitHub][github-samples], que muestran algunos de hello características de mensajería de Bus de servicio de Azure más avanzadas.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
