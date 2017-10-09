---
title: aaaMonitor de estado y alertas en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor mantenimiento y alertas en la pila de Azure."
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a>Supervisar el estado y las alertas en Azure Stack

Pila de Azure incluye infraestructura de supervisión de funciones que permiten a un estado de tooview de operador en la nube y las alertas de una región de la pila de Azure.

Pila de Azure tiene un conjunto de capacidades de administración de región disponibles en hello **administración región** icono. Este icono, anclado de forma predeterminada en el portal de administración de Hola para hello suscripción a proveedor de forma predeterminada, enumera todas las regiones de hello implementado de pila de Azure. También se muestra el recuento de Hola de alertas activas de críticas y de advertencia para cada región. Este icono es el punto de entrada de estado de Hola y alerta de funcionalidad de pila de Azure.

 ![icono de administración de la región de Hola](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a>Comprender el estado en Azure Stack

 Mantenimiento y alertas se administran en la pila de Azure por el proveedor de recursos de mantenimiento de Hola. Componentes de la infraestructura de pila Azure registran con el proveedor de recursos de mantenimiento de Hola durante la configuración e implementación de la pila de Azure. Este registro permite mostrar hello de estado y alertas para cada componente. El estado en Azure Stack es un concepto simple. Si Hola de alertas para una instancia registrada condiciones de un componente, el estado de dicho componente refleja Hola peor active gravedad de alerta; advertencia o crítico.
 
 ## <a name="view-and-manage-component-health-state"></a>Ver y administrar el estado de mantenimiento de un componente
 
 Puede ver el estado de mantenimiento de Hola de componentes en ambos portal del Administrador de pila de Azure de Hola y a través de la API de Rest y PowerShell.
 
estado de mantenimiento de tooview hello en el portal de hello, haga clic en que desea tooview Hola de región de hello **administración región** icono. Puede ver el estado de mantenimiento de Hola de roles de infraestructura y de proveedores de recursos. Tenga en cuenta que en esta versión, proveedor de recursos de proceso de hello no notifica el estado.

![Lista de roles de infraestructura](media/azure-stack-monitor-health/image2.png)

Puede hacer clic en un tooview de rol de infraestructura o el proveedor de recursos información más detallada.

> [!WARNING]
>Si hace clic en un rol de infraestructura y, a continuación, haga clic en la instancia de rol de hello, hay opciones en hello **instancia de rol** tooStart hoja, reinicio o apagado. **No** utilice estas opciones en un entorno de Azure Stack Development Kit. Estas opciones están diseñadas únicamente para un entorno de varios nodos, donde hay más de una instancia de rol por rol de infraestructura. Al reiniciar una instancia de rol (especialmente AzS-Xrp01) en el kit de desarrollo de hello provoca inestabilidad del sistema. Solución de problemas, publique su problema toohello [foro de Azure pila](https://aka.ms/azurestackforum).
>
 
## <a name="view-alerts"></a>Visualización de alertas

lista de Hola de alertas activas para cada región de la pila de Azure está disponible directamente desde hello **administración región** hoja. primer mosaico en la configuración predeterminada de hello Hello es hello **alertas** aparezca como mosaico que muestra un resumen de hello crítico y alertas de advertencia para la región de Hola. Puede anclar el icono de alertas de hello, al igual que cualquier otro icono en esta hoja, panel de toohello para un acceso rápido.   

![Ventana Alerts que muestra una advertencia](media/azure-stack-monitor-health/image3.png)

Mediante la selección en la parte superior del programa Hola Hola **alertas** icono, navegue toohello lista de todas las alertas activas para la región de Hola. Si selecciona cualquier hello **crítico** o **advertencia** artículo de línea en el icono de hello, navegar tooa filtrada la lista de alertas (crítico o advertencia). 

![Alertas de advertencia filtradas](media/azure-stack-monitor-health/image4.png)
  
Hola **alertas** hoja admite Hola capacidad toofilter tanto en gravedad (crítico o advertencia) y el estado (activa o cerrada). vista predeterminada de Hello muestra todas las alertas activas. Todas las alertas cerradas se quitan del sistema de hello después de siete días.

![Toofilter del panel de filtro por estado crítico o de advertencia](media/azure-stack-monitor-health/image5.png)

hoja de alertas de Hello también expone hello **API de vista** acción, ver qué hello muestra API de Rest que era usado toogenerate Hola lista. Esta acción proporciona un familiarizado con la sintaxis de la API de Rest de Hola que puede usar las alertas de tooquery toobecome de forma rápida. Puede utilizar esta API para automatización o para integración con las soluciones existentes de supervisión, informe y vales del centro de datos. 

![Hola opción de API de vista que muestra hello API de Rest](media/azure-stack-monitor-health/image6.png)

Desde la hoja de alertas de hello, puede seleccionar una alerta toonavigate toohello **detalles de alerta** hoja. Esta hoja muestra todos los campos que están asociados a la alerta de Hola y permite una navegación rápida toohello afectadas componente y origen de alerta de Hola. Por ejemplo, hello alerta siguiente se produce si una de las instancias de rol de infraestructura de Hola se queda sin conexión o no está accesible.  

![hoja de detalles de la alerta de Hola](media/azure-stack-monitor-health/image7.png)

Después de instancia de rol de infraestructura de hello es nuevo en línea, esta alerta se cierra automáticamente.

## <a name="next-steps"></a>Pasos siguientes

[Administrar las actualizaciones en Azure Stack](azure-stack-updates.md)

[Administración de regiones en Azure Stack](azure-stack-region-management.md)
