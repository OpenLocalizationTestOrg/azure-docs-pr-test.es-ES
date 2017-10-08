---
title: recomendaciones de Advisor costo aaaAzure | Documentos de Microsoft
description: Utilice el Asistente de Azure toooptimize Hola coste de las implementaciones de Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Recomendaciones sobre el costo de Advisor

Advisor lo ayuda a optimizar y reducir el gasto global de Azure mediante la identificación de recursos inactivos e infrautilizados. Puede obtener costo recomendaciones de hello **costo** pestaña Panel de Asistente de Hola.

![Pestaña Cost (Costo) de Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Optimización del gasto en máquinas virtuales mediante la adecuación del tamaño en instancias infrautilizadas 
Aunque pueden dar lugar a determinados escenarios de aplicación en un uso escaso por diseño, a menudo puede ahorrar dinero mediante la administración del tamaño de Hola y el número de las máquinas virtuales. Advisor supervisa la utilización de las máquinas virtuales durante 14 días e identifica aquellas con una utilización escasa. Se considera que una máquina virtual tiene una utilización escasa si su utilización de la CPU es del 5 % o menos y el de la red es de 7 MB o menos durante cuatro o más días.

El asistente muestra de Hola costo estimado de continuar toorun la máquina virtual, para que pueda elegir tooshut abajo o cambiar su tamaño.  

![Recomendaciones sobre el costo de Advisor para cambiar el tamaño de máquinas virtuales](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Usar un objetivos de rendimiento de la solución más rentable toomanage de varias bases de datos SQL
Advisor identifica las instancias de SQL Server que pueden beneficiarse de la creación de grupos de bases de datos elásticas. Los grupos de bases de datos elásticas proporcionan una solución simple y rentable toomanage objetivos de rendimiento de Hola de varias bases de datos que tienen diferentes patrones de uso. Para más información sobre los grupos de bases de datos elásticas de Azure, consulte [¿Qué es un grupo elástico de Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)

![Recomendaciones sobre el costo de Advisor para grupos de bases de datos elásticas](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>¿Cómo tooaccess costo recomendaciones en el Asistente de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En el panel izquierdo de hello, haga clic en **más servicios**.

3. Hola servicio panel de menú, en **supervisión y administración**, haga clic en **Asistente de Azure**.  
 Hola Advisor panel se abre.

4. En el panel del Asistente de hello, haga clic en hello **costo** ficha.

5. Seleccione la suscripción de hello para el que desea tooreceive recomendaciones y, a continuación, haga clic en **obtener recomendaciones**.

> [!NOTE]
> tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente. Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón. Esta operación *solo se realiza una vez*. Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de las recomendaciones del asistente, vea:
* [Introducción tooAdvisor](advisor-overview.md)
* [Introducción](advisor-get-started.md)
* [Recomendaciones sobre rendimiento de Advisor](advisor-cost-recommendations.md)
* [Recomendaciones sobre alta disponibilidad de Advisor](advisor-cost-recommendations.md)
* [Recomendaciones sobre seguridad de Advisor](advisor-cost-recommendations.md)
