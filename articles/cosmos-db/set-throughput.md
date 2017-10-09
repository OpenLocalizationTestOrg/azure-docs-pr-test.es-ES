---
title: rendimiento de aaaProvision de base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset había aprovisionado containsers, colecciones, gráficos y tablas de base de datos de Azure Cosmos para el rendimiento."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Configuración del rendimiento para contenedores de Azure Cosmos DB

Puede configurar rendimiento para los contenedores de la base de datos de Azure Cosmos Hola portal de Azure o mediante el uso de Hola SDK de cliente. 

Hello en la tabla siguiente enumera rendimiento Hola disponible para los contenedores:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Contenedor de una única partición</strong></p></td>
            <td valign="top"><p><strong>Contenedor con particiones</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Procesamiento mínimo</p></td>
            <td valign="top"><p>400 unidades de solicitud por segundo</p></td>
            <td valign="top"><p>2 500 unidades de solicitud por segundo</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Procesamiento máximo</p></td>
            <td valign="top"><p>10 000 unidades de solicitud por segundo</p></td>
            <td valign="top"><p>Sin límite</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>rendimiento de hello tooset mediante el uso de hello portal de Azure

1. En una nueva ventana, abra hello [portal de Azure](https://portal.azure.com).
2. En la barra de la izquierda hello, haga clic en **base de datos de Azure Cosmos**, o haga clic en **más servicios** en la parte inferior de hello, a continuación, desplácese demasiado**bases de datos**y, a continuación, haga clic en **base de datos de Azure Cosmos**.
3. Seleccione la cuenta de Cosmos DB.
4. En la ventana nueva hello, haga clic en **Explorador de datos (vista previa)** en el menú de navegación de Hola.
5. En la ventana nueva Hola, expanda la base de datos y el contenedor y, a continuación, haga clic en **escala y configuración**.
6. En la ventana nueva Hola escriba Hola nuevo valor de rendimiento en hello **rendimiento** cuadro y, a continuación, haga clic en **guardar**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>rendimiento de hello tooset mediante el uso de hello API de documentos para .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Preguntas más frecuentes sobre el rendimiento

**¿Puedo configurar a mi que no requiere herramientas de rendimiento de 400 RU/s?**

400 RU/s es el rendimiento mínimo de hello disponible en las recopilaciones de una sola partición de base de datos de Cosmos (2500 RU/s es hello mínima para las colecciones particionadas). Solicitar unidades se establecen en intervalos de 100 RU/s, pero el rendimiento no se puede establecer too100 RU/s o cualquier valor menor que 400 RU/s.. Si está buscando un método rentable toodevelop y probar la base de datos de Cosmos, puede usar hello libre [emulador de base de datos de Azure Cosmos](local-emulator.md), que puede implementar localmente sin costo alguno. 

**¿Cómo se configura througput con hello MongoDB API?**

No hay ningún rendimiento tooset de extensión de API de MongoDB. Hello recomendación es toouse hello API de documentos, como se muestra en [tooset el rendimiento de hello mediante el uso de hello API de documentos para .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Pasos siguientes

toolearn más información sobre el aprovisionamiento y escala planeta continuo con la base de datos de Cosmos, consulte [particiones y escalado con la base de datos de Cosmos](partition-data.md).
