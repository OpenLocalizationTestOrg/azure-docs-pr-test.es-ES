---
title: aaaMonitor aplicaciones de servicio de aplicaciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor aplicaciones de servicio de aplicaciones de Azure mediante el uso de Hola Portal de Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Supervisión de Aplicaciones en Azure App Service
[Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714) proporciona funcionalidad de supervisión incorporada en hello [Portal de Azure](https://portal.azure.com).
Esto incluye Hola capacidad tooreview **cuotas** y **métricas** para una aplicación, así como Hola plan de servicio de aplicaciones, configurar **alertas** e incluso **deajustedeescala** automáticamente en función de estas métricas.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Descripción de cuotas y métricas
### <a name="quotas"></a>Cuotas
Las aplicaciones hospedadas en el servicio de aplicaciones son sujeto toocertain *límites* en los recursos que pueden utilizar. Hello define los límites hello **plan de servicio de aplicaciones** asociado a la aplicación hello.

Si la aplicación hello se hospeda en un **libre** o **Shared** previsto, a continuación, define los límites de hello en recursos de hello puede utilizar la aplicación hello **cuotas**.

Si la aplicación hello se hospeda en un **básica**, **estándar** o **Premium** previsto, a continuación, se establecen límites de hello en los recursos de hello pueden utilizar por hello **tamaño** (Pequeño, mediano y grande) y **el número de instancias** (1, 2, 3,...) de hello **plan de servicio de aplicaciones**.

Las **cuotas** de las aplicaciones **gratis** o **compartidas** son:

* **CPU (Short)**
  * Cantidad de CPU permitida para esta aplicación en un intervalo de cinco minutos. Esta cuota se vuelve a establecer cada cinco minutos.
* **CPU (Day)**
  * Cantidad total de CPU permitida para esta aplicación en un día. Esta cuota se vuelve a establecer cada 24 horas a medianoche (UTC).
* **Memoria**
  * Cantidad total de memoria permitida para esta aplicación.
* **Ancho de banda**
  * Cantidad total de ancho de banda saliente permitido para esta aplicación en un día.
    Esta cuota se vuelve a establecer cada 24 horas a medianoche (UTC).
* **Sistema de archivos**
  * Cantidad total de almacenamiento permitido.

Hola solo cuota aplicable tooapps hospedadas en **básica**, **estándar** y **Premium** planes es **Filesystem**.

Obtener más información sobre cuotas específicas de hello, límites y características disponibles para Hola diferentes SKU de servicio de aplicación puede encontrarse aquí: [los límites de servicio de suscripción de Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Aplicación de cuotas
Si una aplicación en su uso supera hello **CPU (corto)**, **CPU (día)**, o **ancho de banda** aplicación de cuota, a continuación, Hola se detendrá hasta que vuelve a establece la cuota de Hola. Durante este tiempo, todas las solicitudes entrantes provocarán un error **HTTP 403**.
![][http403]

Si Hola aplicación **memoria** se supera la cuota, a continuación, aplicación hello se reiniciará.

Si hello **Filesystem** se supera la cuota, a continuación, cualquier escritura que se producirá un error en la operación, se incluye la escritura toologs.

Las cuotas se pueden incrementar o quitar de la aplicación actualizando el plan de App Service.

### <a name="metrics"></a>Métricas
**Las métricas** proporcionan información sobre la aplicación hello y comportamiento del plan de servicio de aplicaciones.

Para una **aplicación**, métricas de hello disponibles son:

* **Tiempo de respuesta promedio**
  * tiempo promedio de Hello necesario para las solicitudes de hello aplicación tooserve en milisegundos.
* **Espacio de trabajo de memoria promedio**
  * promedio de Hola de memoria en MIB utilizados por la aplicación hello.
* **Tiempo de CPU**
  * cantidad de Hola de CPU en segundos consumidos por la aplicación hello. Para más información acerca de esta métrica, consulte [Tiempo de CPU y porcentaje de CPU](#cpu-time-vs-cpu-percentage).
* **Entrada de datos**
  * cantidad de Hola de ancho de banda entrante consumida por la aplicación hello en MIB.
* **Salida de datos**
  * cantidad de Hola de ancho de banda saliente utilizado por la aplicación hello en MIB.
* **Http 2xx**
  * Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 200 e inferior a 300.
* **Http 3xx**
  * Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 300 e inferior a 400.
* **Http 401**
  * Cantidad total de solicitudes que devuelven el código de estado HTTP 401.
* **Http 403**
  * Cantidad total de solicitudes que devuelven el código de estado HTTP 403.
* **Http 404**
  * Cantidad total de solicitudes que devuelven el código de estado HTTP 404.
* **Http 406**
  * Cantidad total de solicitudes que devuelven el código de estado HTTP 406.
* **Http 4xx**
  * Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 400 e inferior a 500.
* **Errores de servidor HTTP**
  * Cantidad total de solicitudes que devuelven un código de estado HTTP superior a 500 e inferior a 600.
* **Espacio de trabajo de memoria**
  * Cantidad actual de memoria utilizada por la aplicación hello en MIB.
* **Solicitudes**
  * Número total de solicitudes, independientemente de su código de estado HTTP resultante.

Para una **plan de servicio de aplicaciones**, métricas de hello disponibles son:

> [!NOTE]
> Las métricas de plan de App Service solo están disponibles para planes de SKU **básico**, **estándar** o **premium**.
> 
> 

* **Porcentaje de CPU**
  * Hola promedio de CPU utilizado por todas las instancias del plan de Hola.
* **Porcentaje de memoria**
  * Hola promedio de memoria usado en todas las instancias del plan de Hola.
* **Entrada de datos**
  * Hola promedio entrantes ancho de banda utilizado por todas las instancias del plan de Hola.
* **Salida de datos**
  * promedio de Hello ancho de banda utilizado por todas las instancias del plan de Hola de salida.
* **Longitud de la cola de disco**
  * promedio de Hola de tanto lectura y escritura de las solicitudes que se pusieron en cola en el almacenamiento. Una longitud de cola de disco alta es una indicación de una aplicación que se podría ralentizar debido tooexcessive de E/S de disco.
* **Longitud de la cola HTTP**
  * promedio de Hola de solicitudes HTTP que tenía toosit en cola Hola antes de que se cumplen. Una longitud de la cola HTTP elevada o creciente indica que un plan está sobrecargado.

### <a name="cpu-time-vs-cpu-percentage"></a>Tiempo de CPU y porcentaje de CPU
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

Hay 2 métricas que reflejan el uso de CPU. **Tiempo de CPU** y **Porcentaje de CPU**

**Tiempo de CPU** es útil para las aplicaciones hospedadas en **libre** o **Shared** planes como uno de sus cuotas se define en minutos de CPU utilizados por la aplicación hello.

**Porcentaje de CPU** en hello otro lado es útil para las aplicaciones hospedadas en **básica**, **estándar** y **premium** planes desde que se pueden escalar horizontalmente y esta métrica es una buena indicación de hello el uso general en todas las instancias.

## <a name="metrics-granularity-and-retention-policy"></a>Directiva de retención y granularidad de métricas
Las métricas para un plan de servicio de aplicación y la aplicación se registran y agregadas por el servicio de hello con hello siguientes granularidades y las directivas de retención:

* Las métricas de granularidad de **minuto** se conservan durante **48 horas**.
* Las métricas de granularidad de **hora** se conservan durante **30 días**.
* Las métricas de granularidad de **día** se conservan durante **90 días**.

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Supervisión de las cuotas y las métricas en hello Portal de Azure.
Puede revisar el estado de Hola de hello diferentes **cuotas** y **métricas** que afectan a una aplicación Hola [Portal de Azure](https://portal.azure.com).

![][quotas]
Las **cuotas** se encuentran en Configuración &gt;**Cuotas**. Hola UX permite revisar: nombre de las cuotas de hello (1), (2) su intervalo de restablecimiento, (3) el límite actual y el valor (4) actual.

![][metrics]
**Las métricas** es posible acceder a directamente desde la hoja de recursos de Hola. También puede personalizar el gráfico de Hola por: (1) **haga clic en** en la base de datos y seleccione (2) **Editar gráfico**.
Desde aquí puede cambiar hello (3) **el intervalo de tiempo**, (4) **tipo de gráfico**y (5) **métricas** toodisplay.  

Para más información acerca de las métricas, consulte [Supervisión de las métricas del servicio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Alertas y autoescala
Las métricas para un plan de aplicación o servicio de aplicaciones puede enlazarse tooalerts, toolearn más detalles al respecto, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Las aplicaciones de App Service hospedadas en planes de App Service básicos, estándar o premium admiten la **autoescala**. Esto permite tooconfigure reglas que supervisan las métricas del plan de servicio de aplicaciones y pueden aumentar o reducir el número de instancias de hello proporciona recursos adicionales según sea necesario o guardando dinero cuando aplicación hello es aprovisionar excesivo. Puede aprender más acerca de la escala automática aquí: [cómo tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) y aquí [las prácticas recomendadas para el ajuste automático del Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
