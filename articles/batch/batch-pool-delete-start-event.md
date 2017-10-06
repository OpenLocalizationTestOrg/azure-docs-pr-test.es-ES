---
title: "aaa \"evento de inicio de eliminación de grupo de lote de Azure | Documentos de Microsoft\""
description: "Referencia del evento de inicio de eliminación de grupo de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>Evento de inicio de eliminación del grupo

 Este evento se genera cuando se inicia una operación de eliminación del grupo. Puesto que la eliminación de grupo de hello es un evento asíncrono, puede esperar un toobe de evento complete de eliminación de grupo genera una vez que la operación de eliminación de hello completa.

 Hello en el ejemplo siguiente se muestra hello cuerpo de un evento de inicio de eliminación de grupo.

```
{
    "id": "myPool1"
}
```

|Elemento|Tipo|Notas|
|-------------|----------|-----------|
|id|String|Hola Id. de grupo de Hola.|
