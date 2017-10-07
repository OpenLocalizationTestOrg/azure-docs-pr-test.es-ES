---
ms.assetid: 
title: "Guía de limitación de almacén de claves aaaAzure | Documentos de Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Guía de las limitaciones de Azure Key Vault

Limitación es un proceso inicia que limita el número de Hola de llamadas concurrentes toohello servicio de Azure tooprevent el uso excesivo de recursos. Almacén de claves de Azure (claves) es toohandle diseñado un gran volumen de solicitudes. Si se produce un número excesivo de solicitudes, la limitación de peticiones de su cliente le ayuda a mantener un rendimiento óptimo y la confiabilidad del programa Hola a servicio de claves.

Límites de limitación varían según el escenario de Hola. Por ejemplo, si está realizando un gran volumen de escrituras, posibilidad de hello para la limitación es mayor que si solo va a realizar lecturas.

## <a name="how-does-key-vault-handle-its-limits"></a>¿Cómo maneja Key Vaults sus límites?

Límites de servicio en el almacén de claves existen tooprevent el uso indebido de los recursos y garantizan la calidad de servicio para todos los clientes del almacén de claves. Cuando se supera un umbral de servicio, Key Vault limita las solicitudes sucesivas de ese cliente durante un período de tiempo. Cuando esto sucede, el almacén de claves devuelve código de estado HTTP 429 (demasiados muchas solicitudes), y Hola solicita producirá un error. Además, no se pudo las solicitudes que devuelven un recuento 429 hacia límites Hola hace un seguimiento mediante el almacén de claves. 

Si tiene un caso empresarial válido para limitaciones superiores, póngase en contacto con nosotros.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>¿Cómo toothrottle la aplicación en respuesta tooservice limita

Hello siguientes son **prácticas recomendadas** para la limitación de la aplicación:
- Reducir el número de Hola de operaciones por solicitud.
- Reduzca la frecuencia de Hola de solicitudes.
- Evite los reintentos inmediatos. 
    - Todas las solicitudes se acumulan en los límites de utilización.

Al implementar el control de errores de la aplicación, use Hola HTTP error código 429 toodetect Hola necesario para la limitación de cliente. Si la solicitud de hello vuelve a falla con un código de error HTTP 429, todavía se está produciendo un límite de servicio de Azure. Continuar toouse Hola recomienda método limitación del cliente, reintentar la solicitud de hello hasta que lo consiga.

### <a name="recommended-client-side-throttling-method"></a>Método de limitación del cliente recomendado

En el código de error HTTP 429, comience la limitación del cliente mediante un enfoque de retroceso exponencial:

1. Espere 1 segundo, reintente la solicitud
2. Si todavía está limitado, espere 2 segundos, reintente la solicitud
3. Si todavía está limitado, espere 4 segundos, reintente la solicitud
4. Si todavía está limitado, espere 8 segundos, reintente la solicitud
5. Si todavía está limitado, espere 16 segundos, reintente la solicitud

En este momento, se deben no está recibiendo los códigos de respuesta HTTP 429.

## <a name="see-also"></a>Otras referencias

Para obtener una orientación más profunda de limitación en hello Microsoft Cloud, vea [limitación patrón](https://docs.microsoft.com/azure/architecture/patterns/throttling).

