---
title: "aaaLog análisis de preguntas más frecuentes | Documentos de Microsoft"
description: "Respuestas toofrequently preguntas más frecuentes sobre Hola servicio de análisis de registros de Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Preguntas frecuentes sobre Log Analytics
En este artículo de Microsoft, se presenta una lista de preguntas frecuentes sobre Log Analytics en Microsoft Operations Management Suite (OMS). Si tiene alguna pregunta adicional sobre el análisis de registros, vaya toohello [foro de discusión](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) y publique sus preguntas. Cuando una pregunta es más frecuentes, se agrega toothis artículo para que se puede encontrar rápida y fácilmente.

## <a name="general"></a>General

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>P: ¿Usar análisis de registros hello mismo agente como centro de seguridad de Azure?

A. En principios de junio de 2017, centro de seguridad de Azure comenzó con hello Microsoft Monitoring Agent toocollect y el almacén de datos. más información, consulte toolearn [preguntas más frecuentes de Azure Security Center plataforma migración](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>P: ¿Qué comprobaciones se realizan por hello AD y soluciones de evaluación de SQL?

A. Hello consulta siguiente muestra una descripción de todas las comprobaciones que se llevan a cabo actualmente:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Hello resultados se pueden tooExcel exportado para revisarlos en profundidad.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>P: ¿Por qué aparece algo distinto a *OMS* en la consola de System Center Operations Manager?

R: En función del paquete acumulativo de actualizaciones de Operations Manager que use, es posible que vea un nodo para *System Center Advisor*, *Operational Insights* o *Log Analytics*.

Hola de actualización de la cadena de texto demasiado*OMS* se incluye en un módulo de administración, que debe toobe importar manualmente. texto actual de toosee hello y las funciones, siga las instrucciones de Hola Hola más reciente KB de paquete acumulativo de actualización de System Center Operations Manager artículo y la actualización de hello consola.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>P: ¿Existe alguna versión *local* de Log Analytics?

R.: No. Log Analytics procesa y almacena grandes cantidades de datos. Como un servicio en la nube, análisis de registros es capaz de tooscale-verticalmente si es necesario y evitar cualquier entorno de tooyour de impacto de rendimiento.

Las ventajas adicionales incluyen:
- Microsoft ejecuta la infraestructura de análisis de registros de hello, lo que ahorra costos
- Implementación regular de actualizaciones y correcciones de características.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>P: ¿Cómo se puede solucionar que Log Analytics ya no recopile datos?

R: si usa Hola libre de nivel de precios y ha enviado más de 500 MB de datos en un día, se detenga la recopilación de datos de rest de hello del día de Hola. Límite diario de hello alcanzando un motivo frecuente que análisis de registros deja de recopilar datos o datos aparecen toobe falta.

Log Analytics crea un evento de tipo *Operación* cuando se inicia y se detiene la recopilación de datos. 

Ejecute hello después de consulta de búsqueda toocheck si va a alcanzar el límite diario de Hola y los datos que faltan:`Type=Operation OperationCategory="Data Collection Status"`

Cuando la recopilación de datos se detiene, hello *OperationStatus* es **advertencia**. Cuando la recopilación de datos se inicia, hello *OperationStatus* es **correcto**. 

Hello tabla siguiente describen las razones que se detenga la recopilación de datos y una colección de datos de tooresume acción sugerida:

| Motivo por el que se detiene la recopilación de datos                       | recopilación de datos de tooresume |
| -------------------------------------------------- | ----------------  |
| Se ha alcanzado el límite diario de datos gratuitos<sup>1</sup>       | Espere a que Hola siguiente día colección tooautomatically reinicio, o<br> Plan de tarifa de pago de tooa de cambio |
| La suscripción de Azure está en estado suspendido debido a: <br> Prueba gratuita finalizada <br> Pase para Azure expirado <br> Se ha alcanzado el límite de gasto mensual (por ejemplo, en una suscripción de MSDN o Visual Studio)                          | Convertir tooa suscripción de pago <br> Convertir tooa suscripción de pago <br> Quite el límite o espere a que se restablezca |

<sup>1</sup> si el área de trabajo está en hello libre de nivel de precios, se verá limitado toosending 500 MB de datos por el servicio de toohello de día. Cuando alcance el límite diario de hello, se detenga la recopilación de datos hasta el día siguiente Hola. Los datos enviados mientras la recopilación de datos está detenida no se indexan ni están disponibles para las búsquedas. Cuando la recopilación de datos se reanuda, únicamente se procesan los nuevos datos enviados. 

Log Analytics usa la hora UTC y cada día se inicia a medianoche de esta hora. Si el área de trabajo de hello alcanza el límite diario de hello, el procesamiento se reanudará durante la primera hora de hello siguiente día UTC Hola.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>P: ¿Cómo puedo recibir una notificación cuando se detiene la recopilación de datos?

R: siga los pasos de hello descritos en [crear una regla de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe una notificación cuando se detenga la recopilación de datos.

Al crear la alerta de Hola para cuando se detenga la recopilación de datos, establezca el:
- **Nombre** demasiado*detenida la recopilación de datos*
- **Gravedad** demasiado*advertencia*
- **Consulta de búsqueda** demasiado`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Período de tiempo** demasiado*2 horas*.
- **Frecuencia de alerta** toobe una hora desde que los datos de uso de hello sólo se actualizan una vez por hora.
- **Generar alerta basada en** toobe *número de resultados*
- **Número de resultados** toobe *mayor que 0*

Siga los pasos de hello descritos en [agregar acciones tooalert reglas](log-analytics-alerts-actions.md) configurar una acción de correo electrónico, webhook o runbook de regla de alerta de Hola.


## <a name="configuration"></a>Configuración
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>P: ¿Puedo cambiar nombre de Hola de hello blobs o tablas contenedor utilizado tooread de diagnósticos de Azure (WAD)?

A. No, no es posible actualmente tooread de tablas arbitrarias o contenedores en el almacenamiento de Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>P: ¿Qué direcciones IP Hola uso del servicio de análisis de registros? ¿Cómo me aseguro de que el firewall solo permita el servicio de análisis de registros de tráfico toohello?

A. Hola servicio de análisis de registros se basa en Azure. Direcciones de IP de análisis de registro están en hello [intervalos de IP de centro de datos de Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653).

Según se realizan implementaciones de servicio, cambian las direcciones IP de hello reales de hello servicio de análisis de registros. Hola tooallow de nombres DNS a través del firewall se documentan en [configurar ajustes del proxy y firewall de análisis de registros](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>P: Uso ExpressRoute para la conexión tooAzure. ¿El tráfico de Log Analytics usa la conexión ExpressRoute?

A. Hola distintos tipos de tráfico de ExpressRoute se describen en hello [documentación de ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

Análisis del tráfico tooLog usa circuito de ExpressRoute de emparejamiento público Hola.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>P: ¿Hay una manera simple y fácil toomove un tooanother de área de trabajo de análisis de registros existente suscripción de Azure/área de trabajo de análisis de registros?

A. Hola `Move-AzureRmResource` cmdlet le permite mover un área de trabajo de análisis de registros y también una cuenta de automatización de tooanother de una suscripción de Azure. Para más información, consulte [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Este cambio también se realizó en hello portal de Azure.

No se puede mover los datos de una tooanother de área de trabajo de análisis de registros o cambiar la región de Hola que datos de análisis de registros se almacenan en.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>P: ¿cómo agregar registro análisis tooSystem Center Operations Manager?

R: si aplica toohello paquete acumulativo de actualizaciones más reciente e importar módulos de administración le permiten tooconnect Operations Manager tooLog análisis.

>[!NOTE]
>tooLog de conexión de Operations Manager Hola análisis solo está disponible para System Center Operations Manager 2012 SP1 y versiones posteriores.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>P: ¿Cómo puedo confirmar que un agente es capaz de toocommunicate con análisis de registros?

R: tooensure ese agente Hola pueda comunicarse con OMS, vaya a: Panel de Control, seguridad y configuración, **Microsoft Monitoring Agent**.

En hello **Azure Log Analytics (OMS)** ficha, busque una marca de verificación verde. Un icono de marca de verificación verde confirma que el agente hello es capaz de toocommunicate con hello servicio OMS.

Un icono de advertencia amarillo significa que el agente de hello está teniendo problemas de comunicación con OMS. Un motivo habitual es Hola servicio del agente de supervisión de Microsoft se ha detenido. Usar servicio de service control manager toorestart Hola.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>P: ¿Cómo se detiene la comunicación entre un agente y Log Analytics?

R: en System Center Operations Manager, quitar equipo de Hola de lista de equipos administrados de hello Advisor. Actualizaciones de Operations Manager Hola configuración de hello agente toono más informes tooLog análisis. Para agentes conectados directamente tooLog análisis, se puede impedir que comunicarse a través de: Panel de Control, seguridad y configuración, **Microsoft Monitoring Agent**.
Quite todas las áreas de trabajo enumeradas en **Azure Log Analytics (OMS)**.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>P: ¿por qué recibo un error cuando intento toomove mi área de trabajo de una suscripción de Azure tooanother?

R: Si usas Hola portal de Azure, asegúrese de solo el área de trabajo de Hola Hola move. No seleccione las soluciones de hello, se moverá automáticamente cuando se mueva el área de trabajo de Hola. 

Asegúrese de tener permisos en ambas suscripciones de Azure.

## <a name="agent-data"></a>Datos del agente
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>P: ¿Cuántos datos puedo enviar mediante Hola agente tooLog análisis? ¿Hay una cantidad máxima de datos por cliente?
A. plan de Hello gratuito establece un límite diario de 500 MB por área de trabajo. Hola estándar y planes premium no tienen límites en la cantidad de Hola de datos que se haya cargado. Un servicio de nube, análisis de registros está diseñado escalar tooautomatically volumen de hello toohandle procedente de un cliente, aunque sean terabytes al día.

agente de análisis de registros de Hello fue diseñado tooensure tiene una pequeña superficie. Uno de nuestros clientes escribió un blog sobre las pruebas de Hola que realizaron con nuestro agente y los impresionantes resultados que obtuvieron. volumen de datos de Hello varía en función de soluciones de Hola que se habilita. Puede encontrar información detallada sobre el volumen de datos de Hola y ver Hola descomposición por soluciones en hello [uso](log-analytics-usage.md) página.

Para obtener más información, puede leer un [blog de un cliente](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) sobre baja superficie del agente de OMS Hola de Hola.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>P: ¿Cuánto ancho de banda de red se utiliza Hola agente de administración de Microsoft (MMA) al enviar datos tooLog análisis?

A. Ancho de banda es una función de la cantidad de Hola de los datos enviados. Datos se comprimen a medida que se envía a través de la red de Hola.

### <a name="q-how-much-data-is-sent-per-agent"></a>P: ¿Qué cantidad de datos se envía por agente?

A. cantidad de Hola de los datos enviados por el agente depende de:

* soluciones de Hola que haya habilitado
* número de Hola de registros y que se recopilan los contadores de rendimiento
* volumen de Hola de datos en los registros de Hola

Hola libre tarifa es una buena manera tooonboard varios servidores y medir el volumen de datos típico de Hola. Uso general se muestra en hello [uso](log-analytics-usage.md) página.

Para equipos que son toorun capaz de agente de WireData de hello, utilice Hola después toosee de consulta que se está enviando la cantidad de datos:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Pasos siguientes
* [Empezar a trabajar con análisis de registros](log-analytics-get-started.md) toolearn más información sobre análisis de registros y póngase en marcha en minutos.
