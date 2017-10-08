---
title: aaaManage precios y volumen de datos de Azure Application Insights | Documentos de Microsoft
description: "Administre los volúmenes de telemetría y supervise los costos en Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Administración de precios y volúmenes de datos de Application Insights


Los precios para [Azure Application Insights][start] se basan en el volumen de datos por aplicación. Poca utilización durante el desarrollo o para una aplicación pequeña es probable que toobe libre, porque no hay una deducción mensual de 1 GB de datos de telemetría.

Cada recurso de Application Insights se carga como un servicio independiente y contribuye toohello factura para su tooAzure de suscripción.

Hay dos planes de precios. plan de Hello predeterminado se denomina Basic. Puede optar por plan empresarial de hello, que tiene un cargo diario, pero permite que determinadas características adicionales como [exportación continua](app-insights-export-telemetry.md).

Si tiene alguna pregunta acerca del funcionamiento de precios para Application Insights, sentirse toopost libre una pregunta en nuestros [foro](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>planes de precios de Hola

Vea hello [Application Insights página de precios] [ pricing] para los precios actuales en su moneda.

### <a name="basic-plan"></a>Plan Básico

plan básico de Hello es predeterminado de hello cuando se crea un nuevo recurso de Application Insights y será suficiente para la mayoría de los clientes.

* En el plan básico de hello, se le cobra por volumen de datos: número de bytes de telemetría recibidos por Application Insights. Volumen de datos se mide como tamaño de Hola Hola sin comprimir JSON del conjunto de datos recibido por Application Insights de la aplicación.
Para [importados en análisis de datos tabulares](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), volumen de datos de Hola se mide como Hola tamaño descomprimido de archivos enviados tooApplication visión.  
* El primer 1 GB para cada aplicación está disponible, para que si simplemente experimentar o desarrollar, que sea improbable toohave toopay.
* Los datos de la [secuencia de métricas en directo](app-insights-live-stream.md) no cuentan para calcular los precios.
* [Exportación continua](app-insights-export-telemetry.md) está disponible para un cargo adicional por cada GB en el plan básico de Hola.

### <a name="enterprise-plan"></a>Plan Enterprise

* En el plan de empresa de hello, puede usar todas las características de Hola de Application Insights para su aplicación. La [exportación continua](app-insights-export-telemetry.md) y 

[Conector de análisis de registro](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) están disponibles sin ningún cargo adicional en el plan de hello empresarial.
* Se paga por nodo que está enviando la telemetría para las aplicaciones en el plan de la empresa de Hola. 
 * Un *nodo* es un servidor físico o virtual o una instancia de rol de plataforma como servicio que hospeda su aplicación.
 * Los equipos de desarrollo, los exploradores cliente y los dispositivos móviles no se cuentan como nodos.
 * Si su aplicación presenta varios componentes que envían telemetría, como un servicio web y un trabajo de back-end, se cuentan por separado.
 * Los datos de [Live Metrics Stream](app-insights-live-stream.md) no cuentan para calcular los precios.* En una suscripción, sus cargos son por nodo, no por aplicación. Si tiene cinco nodos enviar telemetría para 12 aplicaciones, a continuación, Hola cobra es de cinco nodos.
* Aunque los cargos se presupuestan mensualmente, solo se le cobrarán las horas en las que un nodo envíe telemetría de una aplicación. Hola cargo por hora es Hola entrecomillados cargo mensual / 744 (Hola número de horas en un mes de 31 días).
* Se proporciona una asignación de volumen de datos de 200 MB por día para cada nodo detectado (con una granularidad de horas). La asignación de datos no utilizados no se realiza a través de un día toohello junto.
 * Si elige Hola opción de precios de Enterprise, cada suscripción Obtiene una deducción diaria de datos según el número de Hola de nodos enviar telemetría toohello recursos de Application Insights en esa suscripción. Por lo que si tiene 5 nodos enviar datos de todo el día, tendrán una deducción de 1 GB aplica tooall Hola Application Insights recursos agrupada en esa suscripción. No importa si determinados nodos están enviando que datos más que otros nodos porque Hola incluía datos se comparten entre todos los nodos. Si, en un día determinado, recursos de Application Insights Hola recibirán más datos de los que se incluye en la asignación de datos diario Hola para esta suscripción, se aplican cargos de datos por encima del límite de Hola por GB. 
 * asignación de datos diario Hola se calcula como número de Hola de horas en hello día de inicio (UTC) que cada nodo está enviando telemetría dividido entre 200 MB de 24 horas. Por tanto, si tiene 4 nodos enviar telemetría durante 15 de hello 24 horas del día de hello, Hola incluye datos para ese día sería ((4 x 15) / 24) x 200 MB = 500 MB. En el precio de Hola de 2.30 USD por GB por exceso de uso de datos, gratuito Hola sería USD 1.15 si 1 GB de datos, los nodos de hello enviar ese día.
 * Tenga en cuenta que asignación diaria del plan de hello empresarial no se comparte con las aplicaciones para el que ha elegido la opción básica de Hola y asignación sin usar no se traslada de diarias. 
* Estos son algunos de los ejemplos de cómo determinar el número concreto de nodos:
| Escenario                               | Número de nodos total diario |
|:---------------------------------------|:----------------:|
| 1 aplicación está usando 3 instancias de Azure App Service y 1 servidor virtual. | 4 |
| 3 aplicaciones que se ejecutan en 2 máquinas virtuales y recursos de Application Insights de Hola para estas aplicaciones están en Hola misma suscripción y Hola Enterprise planear | 2 | 
| 4 aplicaciones cuyos recursos de información de las aplicaciones están en Hola misma suscripción. Cada aplicación ejecuta 2 instancias durante 16 horas de poca actividad y 4 durante 8 horas de máxima actividad. | 13,33 | 
| Servicios en la nube con 1 rol de trabajo y 1 rol web; cada uno ejecuta 2 instancias. | 4 | 
| Clúster de Service Fabric de 5 nodos que ejecuta 50 microservicios; cada uno de estos últimos ejecuta 3 instancias. | 5|

* el comportamiento de recuento de nodo precisa Hola depende de en el que está usando el SDK de visión de aplicación de la aplicación. 
  * En las versiones SDK 2.2 y y versiones posteriores, ambos Hola Application Insights [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) o [SDK Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) van a cada host de aplicación como un nodo de informes, por ejemplo Hola nombre de equipo para el servidor físico y los hosts de VM o hello nombre de la instancia en caso de hello de servicios en la nube.  Hola única excepción es aplicaciones solamente con [.NET Core](https://dotnet.github.io/) hello Application Insights Core SDK, en la que un único nodo case se notificará para todos los hosts porque no está disponible el nombre de host de Hola y. 
  * Para las versiones anteriores de hello SDK, Hola [SDK Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) se comportará igual hello las versiones más recientes de SDK, sin embargo Hola [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) informará de un único nodo, independientemente del número de Hola de hosts de aplicación real. 
  * Tenga en cuenta que si la aplicación está utilizando el valor personalizado de hello SDK tooset roleInstance tooa, de forma predeterminada ese mismo valor se utiliza el recuento de hello toodetermine de nodos. 
  * Si utilizas una nueva versión SDK con una aplicación que se ejecuta desde dispositivos móviles o equipos cliente, es posible que el recuento de Hola de nodos podría devolver un número que es muy grande (de hello gran número de dispositivos móviles o equipos cliente). 

### <a name="multi-step-web-tests"></a>Pruebas web de varios pasos

Se realiza un cargo adicional para las [pruebas web de varios pasos](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Esto refiere tooweb pruebas que ejecute una secuencia de acciones. 

No hay ningún cargo aparte para las "pruebas de ping" de una sola página. La telemetría de las pruebas de ping y de las de varios pasos se carga junto con el resto de la telemetría de su aplicación.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Derechos de suscripción de Operations Management Suite

Como [anunció recientemente](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), los clientes que compran Microsoft Operations Management Suite E1 y E2 son tooget capaz de aplicación visión empresarial como un componente adicional sin ningún costo adicional. En concreto, cada unidad de Operations Management Suite E1 y E2 incluye un nodo de too1 de derechos de plan empresarial de Hola de Application Insights. Como se mencionó anteriormente, cada nodo de Application Insights incluye too200 MB de datos ingeridos por día (independiente de la recopilación de datos de análisis de registros), con la retención de datos de 90 días sin costo adicional alguno. 

> [!NOTE]
> tooensure que obtiene este derecho, debe tener los recursos de Application Insights de empresa de hello plan de precios. Este derecho se aplica solo como nodos, por lo que los recursos de Application Insights en el plan básico de Hola no obtendrán ninguna ventaja. Tenga en cuenta que este derecho no estarán visible en hello estimado costos mostrados en las características de hello + hoja de precios. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Revisión de los planes de precios y cálculo de costos

Visión Applicaition facilita hello toounderstand fácil precios planes disponibles y qué Hola costes son probablemente puede basarse en patrones de uso reciente. Comience por abrir hello **características + precios** hoja Hola recurso de Application Insights en hello portal de Azure:

![Elija el precio.](./media/app-insights-pricing/01-pricing.png)

**a.** Revise el volumen de datos para el mes de Hola. Esto incluye todos los datos de hello recibido y conservan (después de un [muestreo](app-insights-sampling.md) desde las aplicaciones de cliente y servidor y de pruebas de disponibilidad.

**b.** Se realiza un cargo adicional para las [pruebas web de varios pasos](app-insights-monitor-web-app-availability.md#multi-step-web-tests). (Esto no incluye pruebas de disponibilidad simple, que se incluyen en la carga de volumen de datos de Hola.)

**c.** Habilitar plan empresarial de Hola.

**d.** Desplazarse por volumen de datos de toodata administración opciones tooview para hello último mes, establezca un límite diario o muestreo de recopilación.

Los cargos de visión de aplicación se agregan tooyour factura de Azure. Puede ver detalles de su Azure facturar en la sección de facturación de hello portal de Azure o en Hola Hola [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![En el menú del lado de hello, elija la facturación.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Velocidad de datos
Hay tres maneras de en qué Hola se limita volumen enviar datos:

* **Muestreo:** se puede utilizar este mecanismo Acorte Hola enviado desde las aplicaciones cliente y servidor, con la mínima distorsión de las métricas de telemetría. Se trata de herramienta principal de hello tiene tootune Hola cantidad de datos. Obtenga más información sobre las [características de muestreo](app-insights-sampling.md). 
* **Límite diario:** cuando la creación de un recurso de Application Insights de hello portal de Azure esto está establecida a too500 GB/día. Hola de forma predeterminada al crear un recurso de información de la aplicación desde Visual Studio, es pequeño (solo 32,3 MB/día) que está pensado solo toofaciliate pruebas. En este caso está dirigida a que ese usuario Hola generará límite diario de hello antes de implementar la aplicación hello en producción. límite máximo de Hello es 500 GB/día a menos que se ha solicitado una máxima más alta para una aplicación de mucho tráfico. Tenga cuidado al establecer el límite diario de hello, ya que debe ser su intención **nunca las límite diario de las hello toohit**, ya que, a continuación, se pierdan los datos para el resto de hello del día de Hola y ser toomonitor no se puede la aplicación. toochange lo, hoja de cap de volumen diario de uso hello, vinculada del programa de hoja de administración de volúmenes de datos de hello (ver abajo). Tenga en cuenta que algunos tipos de suscripción disponen de un crédito que no se puede usar para Application Insights. Si suscripción hello tiene gasto limitar, Hola diariamente hoja cap tendrá instrucciones cómo tooremove y habilitar Hola diaria toobe cap generado más allá del 32,3 MB/día.  
* **Limitación:** este límites Hola datos tasa too32 k eventos por segundo, promedio durante más de 1 minuto. 


*¿Qué ocurre si mi aplicación supera la limitación de velocidad de hello?*

* volumen de Hola de datos que envía la aplicación se evalúa cada minuto. Si supera la tasa por segundo de hello promediada por minuto de hello, servidor de hello rechaza algunas solicitudes. Hola SDK almacena en búfer los datos de hello y, a continuación, intenta tooresend, distribuya una sobrecarga durante varios minutos. Si la aplicación coherente envía datos por encima de la limitación de velocidad de hello, algunos datos se van a quitar. (Hola ASP.NET, Java y JavaScript SDK intentan tooresend de esta manera; otros SDK podría simplemente los datos de colocar limitada). Si se produce la limitación, verá una notificación de advertencia que indica que esto ha sucedido.

*¿Cómo puedo saber cuántos datos envía mi aplicación?*

* Abra hello **administración del volumen de datos** gráfico de volumen de hoja toosee Hola diaria datos. 
* O bien, en el Explorador de métricas, agregue un nuevo gráfico y seleccione **Volumen de punto de datos** como su métrica. Active la agrupación y agrupe por **Tipo de datos**.

## <a name="tooreduce-your-data-rate"></a>tooreduce la velocidad de datos
Estas son algunas cosas que puede hacer tooreduce el volumen de datos:

* Use el [Muestreo](app-insights-sampling.md). Esta tecnología reduce la velocidad de datos sin sesgar las métricas y sin interrumpir Hola capacidad toonavigate entre los elementos relacionados en la búsqueda. En las aplicaciones de servidor, funciona automáticamente.
* [Limitar número de Hola de llamadas de Ajax que se pueden notificar](app-insights-javascript.md#detailed-configuration) en cada vista de página o conmutador desactivar informes de Ajax.
* Desactivar los módulos de recopilación que no necesite; para ello, [edite ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Por ejemplo, podría decidir que los contadores de rendimiento o datos de dependencia no son esenciales.
* Divida las claves de instrumentación de telemetría tooseparate. 
* Métricas agregadas previamente. Si ha colocado tooTrackMetric de llamadas en la aplicación, puede reducir el tráfico mediante el uso de la sobrecarga de Hola que acepta el cálculo de Media de Hola y desviación estándar de un lote de mediciones. O bien, puede usar un [paquete de agregación previa](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>Administrar el volumen de datos máximo diario Hola

Puede utilizar Hola diaria volumen cap toolimit Hola datos recopilados, pero si se cumple la cap de hello, se producirá una pérdida de todos los telemetery enviados desde la aplicación para el resto de hello del día de Hola. Es **no recomienda** toohave su límite diario de aplicación toohit Hola desde que son estado de hello no se puede tootrack y el rendimiento de la aplicación después de que se ejecute. 

En su lugar, use [muestreo](app-insights-sampling.md) tootune Hola datos toohello nivel de volumen que desee y usar límite diario de hello solo como "último recurso" en caso de que la aplicación comienza a enviar más volúmenes de telemetery de forma inesperada. 

Haga clic en toochange límite diario de hello, Hola sección de configuración de los recursos de aplicación Insihgts, **administración del volumen de datos** , a continuación, **límite diario**.

![Ajustar Hola telemetría volumen límite diario](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>muestreo
[Muestreo](app-insights-sampling.md) es un método de reducción de la velocidad de hello en el que telemetría se envía tooyour aplicación, al tiempo que se mantiene Hola capacidad toofind relacionada con eventos durante las búsquedas de diagnóstico y recuentos de eventos apropiado siga conservando. 

El muestreo es una manera eficaz de tooreduce se aplicarán cargos y permanezca dentro de su cuota mensual. Hello algoritmo de muestreo conserva elementos relacionados de telemetría, por lo que, por ejemplo, cuando se usa la búsqueda, puede encontrar excepciones concretas tooa relacionados con la solicitud de Hola. algoritmo de Hello también conserva recuentos correctos, de manera que vea valores correctos hello en el Explorador de métrica de velocidad de solicitudes, tasas de excepción y otros recuentos.

Existen varias formas de muestreo.

* [Muestreo adaptativo](app-insights-sampling.md) es predeterminado de Hola para hello SDK de ASP.NET, que ajusta automáticamente el volumen de toohello de telemetría que envía la aplicación. Su funcionamiento automáticamente en hello SDK en la aplicación web, por lo que se reduce el tráfico de telemetría de hello en red Hola. 
* *Muestreo de ingesta* es una alternativa que se aplica en el punto de Hola donde telemetría desde la aplicación entra en servicio de Application Insights de Hola. No se ve afectada volumen Hola de telemetría enviado desde su aplicación, pero reduce el volumen de hello retenida por el servicio de Hola. Puede usar cuota de hello tooreduce usa telemetría de exploradores y otros SDK de.

tooset ingesta de muestreo, establezca el control de hello en la hoja de precios de hello:

![De cuota de Hola y de hoja de precios, haga clic en el icono de ejemplos de hello y seleccione una fracción de muestreo.](./media/app-insights-pricing/04.png)

> [!WARNING]
> hoja de muestreo de datos de Hello sólo controla el valor Hola de muestreo de recopilación. No reflejar frecuencia de muestreo de Hola que se aplican por hello Application Insights SDK en la aplicación. Si ya se han tomado muestras telemetría de Hola entrantes en hello SDK, no se aplica el muestreo de recopilación.
> 

hello toodiscover real muestreo tasa independientemente de donde se ha aplicado, use un [consulta de análisis](app-insights-analytics.md) como este:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

En cada uno de ellos conserva el registro, `itemCount` indica Hola número de registros original que representa, too1 igual + número de Hola de registros descartados anteriores. 


## <a name="automation"></a>Automation

Puede escribir un plan de precios de secuencia de comandos tooset hello, con administración de recursos de Azure. [Más información](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Resumen de límites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Pasos siguientes

* [Muestreo](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

