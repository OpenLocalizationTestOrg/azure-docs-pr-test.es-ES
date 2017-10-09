---
title: "Explicación de las unidades de proceso en Azure Database for MySQL | Microsoft Docs"
description: "Base de datos de Azure para MySQL: este artículo se explican conceptos de Hola de unidades de proceso y lo que ocurre cuando la carga de trabajo alcanza Hola la capacidad máxima de proceso."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>Explicación de las unidades de proceso en Azure Database for MySQL
Este artículo explica el concepto de Hola de unidades de proceso y lo que ocurre cuando la carga de trabajo alcanza Hola la capacidad máxima de proceso.

## <a name="what-are-compute-units"></a>¿Qué son las unidades de proceso?
Proceso de unidades son una medida de rendimiento de procesamiento de CPU que se garantiza toobe disponible tooa única base de datos de MySQL server. Una unidad de proceso es una medida combinada de recursos de CPU y memoria. En general, 50 unidades de proceso equivaler toohalf de un núcleo. 100 unidades de proceso equivaler tooone core. Unidades de proceso de 2000 equivaler tootwenty núcleos del servidor de procesamiento garantizada rendimiento tooyour disponible.

cantidad de Hola de memoria por unidad de proceso se optimiza para hello Basic y niveles de precios estándar. Duplica Hola proceso unidades aumentando el nivel de rendimiento de hello equivale toodoubling Hola formado por recursos disponibles toothat única base de datos de MySQL.

Por ejemplo, 800 unidades de proceso de un plan Estándar proporcionan 8 veces más rendimiento de CPU y memoria que una configuración Estándar con 100 unidades de proceso. Sin embargo, mientras que las unidades de proceso de 100 estándar ofrecen Hola mismo rendimiento de CPU en comparación con tooBasic 100 unidades de proceso, Hola de memoria que está preconfigurado en el nivel de precios estándar es double Hola cantidad de memoria configurada para el nivel de precios de Basic. Por lo tanto, nivel de precios estándar proporciona un mejor rendimiento de carga de trabajo y menor latencia de las transacciones de nivel de precios básico con hello que mismas unidades de proceso seleccionada.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>¿Cómo se puede determinar el número de Hola de unidades de proceso necesarios para la carga de trabajo?
Si desea toomigrate un servidor MySQL existente que se ejecuta de forma local o en una máquina virtual, puede determinar Hola número de unidades de proceso calculando el número de núcleos del rendimiento de procesamiento de la carga de trabajo necesita. 

Si el servidor del entorno local o de la máquina virtual está usando actualmente 4 núcleos (sin contar el hiperproceso de CPU), empiece por configurar 400 unidades de proceso para el servidor de Azure Database for MySQL. Las unidades de proceso se pueden escalar o reducir verticalmente y de forma dinámica en función de las necesidades de la carga de trabajo sin apenas tiempo de inactividad de las aplicaciones. 

Gráfico de métricas de monitor Hola Hola Azure portal o escritura CLI de Azure comandos - toomeasure unidades de proceso. Toomonitor de métricas pertinente son el porcentaje de la unidad de proceso de Hola y límite de unidad de proceso.

>[!IMPORTANT]
> Si encuentra almacenamiento IOPS no son totalmente utiliza toohello máximo, considere la posibilidad de supervisión de uso de unidades de proceso de hello así. Cuando se genera Hola proceso unidades puede permiten un mayor rendimiento de E/S por lo que reduce cuello de botella de rendimiento de hello debido toolimited CPU o memoria.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>¿Qué ocurre cuando se alcanza el número máximo de unidades de proceso?
Los niveles de rendimiento estén calibrados y rigen tooprovide recursos toorun la carga de trabajo de la base de datos los límites de max toohello de tarifa seleccionado hello y nivel de rendimiento. 

Si la carga de trabajo alcanza los límites máximos de hello en ser Hola proceso unidades o los límites IOPS aprovisionados, puede continuar tooutilize recursos de Hola a nivel máximo permitido de hello, pero las consultas son las latencias de toosee probable aumentado. Estos límites no dan lugar a errores, pero en su lugar una ralentización de la carga de trabajo de hello, a menos que esté tan grave que el tiempo de espera de consulta ralentización Hola. 

Si la carga de trabajo alcanza el límite máximo de hello en número de conexiones, se producen errores explícitos. Para obtener más información sobre los límites de los recursos, consulte [Limitaciones en Azure Database for MySQL](concepts-limits.md).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los planes de tarifa, consulte [Planes de tarifa de Azure Database for MySQL](./concepts-service-tiers.md).
