---
title: "Mapa de la solución aaaService cursos de demostración | Documentos de Microsoft"
description: "Mapa de servicio es una solución en Operations Management Suite (OMS) que detecta automáticamente los componentes de la aplicación en Windows y mapas y sistemas Linux Hola comunicación entre los servicios.  Se trata de una demostración sencilla propia que le guía a través de utilizando el mapa de servicio tooidentify y diagnosticar un problema simulado en una aplicación web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Demostración autodidáctica de Operations Management Suite (OMS): Service Map
Se trata de una demostración sencilla propia que le guía a través mediante hello [mapa de servicio de la solución](operations-management-suite-service-map.md) en tooidentify Operations Management Suite (OMS) y diagnosticar un problema simulado en una aplicación web.  Mapa de servicio detecta automáticamente los componentes de la aplicación en los sistemas Windows y Linux y mapas Hola comunicación entre los servicios.  También consolida los datos recopilados por otro tooassist de servicios OMS que analizar el rendimiento y a identificar problemas.  También podrá usar [búsquedas de registro de análisis de registros](../log-analytics/log-analytics-log-searches.md) toodrill hacia abajo en los datos recopilados en orden tooidentify Hola causa principal del problema.


## <a name="scenario-description"></a>Descripción del escenario
Acaba de recibir una notificación de que la aplicación del Portal de cliente de ACME Hola está teniendo problemas de rendimiento.  Hola única información que tiene es que estos problemas iniciado aproximadamente 4:00 a.m. hora del Pacífico hoy en día.  No está completamente seguro de todos los componentes de hello ese portal hello es dependiente que no sea un conjunto de servidores web.  

## <a name="components-and-features-used"></a>Componentes y características usados
- [Solución Service Map](operations-management-suite-service-map.md)
- [Búsquedas de registros de Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Tutorial

### <a name="1-connect-toohello-oms-experience-center"></a>1. Conecte toohello OMS experiencia Center
Este tutorial usa hello [Operations Management Suite experiencia Center](https://experience.mms.microsoft.com/) que proporciona un completo entorno de OMS con datos de ejemplo. Inicie haciendo clic en el vínculo, proporcione la información de y, a continuación, seleccione hello **una visión general y análisis** escenario.


### <a name="2-start-service-map"></a>2. Inicio de Service Map
Iniciar solución de mapa de servicio de hello haciendo clic en hello **Service Map** icono.

![Icono de Service Map](media/operations-management-suite-walkthrough-servicemap/tile.png)

se muestra la consola de Service Map Hola.  Hola panel izquierdo es una lista de equipos en su entorno con un agente de mapa de servicio de hello instalado.  Deberá seleccionar equipo Hola que desea tooview de esta lista.

![Lista de equipos](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Visualización del equipo
Sabemos que los servidores web Hola se denominan AcmeWFE001 y AcmeWFE002, por lo que esta parece ser un toostart lugar razonable.  Haga clic en **AcmeWFE001**.  Esto muestra el mapa de Hola para AcmeWFE001 y todas sus dependencias.  Puede ver los procesos que se ejecutan en el equipo seleccionado de Hola y que se comunican con los servicios externos.

![Servidor Web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Se le preocupa el rendimiento de Hola de nuestra web aplicación por lo que haga clic en hello **AcmeAppPool (grupo de aplicaciones de IIS)** proceso.  Esto muestra los detalles de Hola de este proceso y resalta sus dependencias.  

![Grupo de aplicaciones](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Cambio de la ventana de tiempo

Escuchamos error Hola iniciada a las 4:00 A.M., así que vamos a Eche un vistazo a lo que estaba sucediendo en ese momento. Haga clic en **intervalo de tiempo** y cambiar Hola tiempo too4: 00 AM PST (mantener Hola fecha actual y ajuste de la zona horaria local) con una duración de 20 minutos.

![Selector de hora](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Visualización de la alerta

Ahora vemos que hello **acmetomcat** dependencia tiene una alerta que aparece, por lo que es el posible problema.  Haga clic en el icono de alerta de hello en **acmetomcat** tooshow detalles de Hola de alerta de Hola.  Podemos ver que tenemos un uso crítico de la CPU y podemos expandirlo para verlo con más detalle.  Esta es probablemente la causa de que nuestro rendimiento sea tan lento. 

![Alerta](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Visualización del rendimiento

Vamos a echar un vistazo más de acerca a **acmetomcat**.  Haga clic en hello superior derecha del **acmetomcat** y seleccione **carga servidor mapa** tooshow Hola detalle y las dependencias de esta máquina. Podemos, a continuación, observar un poco más en esos tooverify de contadores de rendimiento nuestro conjetura.  Seleccione hello **rendimiento** Hola de ficha toodisplay [contadores de rendimiento recopilan por el análisis de registro](../log-analytics/log-analytics-data-sources-performance-counters.md) sobre el intervalo de tiempo de Hola.  Podemos ver que estamos preparando picos periódicos en memoria y el procesador de Hola.

![Rendimiento](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Visualización del seguimiento de cambios
Veamos si podemos descubrir cuál podría ser la causa de esta elevada utilización.  Haga clic en hello **resumen** ficha.  Esto proporciona el error en la información que ha recopilado OMS desde el equipo de hello como conexiones, las alertas críticas y los cambios de software.  Ya deben haberse expandidas secciones con información reciente interesante y puede expandir otra información de tooinspect de secciones que contienen.


Si **Seguimiento de cambios** no está ya abierta, expándala.  Esto muestra la información recopilada por hello [solución de seguimiento de cambios](../log-analytics/log-analytics-change-tracking.md).  Parece que se ha producido un cambio de software durante este período de tiempo.  Haga clic en **Software** tooget detalles.  Un proceso de copia de seguridad se agregó toohello máquina justo después de 4:00 A.M., por lo que esto parece culpable de hello toobe para recursos excesivos de hello consumido.

![Seguimiento de cambios](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Visualización de los detalles en la búsqueda de registros
Podemos comprobar aún más este examinando Hola información de rendimiento recopilada en el repositorio de análisis de registros de hello detallada.  Haga clic en hello **alertas** ficha nuevo y, a continuación, en uno de hello **elevado de la CPU** alertas.  Haga clic en **Mostrar en la búsqueda de registro**.  Se abrirá la ventana de búsqueda de registros de hello donde puede realizar [búsquedas de registro](../log-analytics/log-analytics-log-searches.md) frente a los datos almacenados en el repositorio de Hola.  Mapa de servicio ya ha rellenado en un queriy para que podamos alerta de hello tooretrieve nos interesa.  

![Búsqueda de registros](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Apertura de la búsqueda guardada
Veamos si podemos obtener algunos detalles más en la recopilación de rendimiento de Hola que generó esta alerta y compruebe nuestra sospecha que los problemas de hello están provocados por ese proceso de copia de seguridad.  Cambiar el intervalo de tiempo de hello demasiado**6 horas**.  A continuación, haga clic en **favoritos** y desplácese hacia abajo toohello guardan busca **mapa de servicio**.  Estas son consultas que hemos creado específicamente para este análisis.  Haga clic en **5 principales procesos por uso de CPU para acmetomcat**.

![Búsqueda guardada](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Esta consulta devuelve una lista de hello principales 5 procesos consumen procesador en **acmetomcat**.  Puede inspeccionar Hola consulta tooget un lenguaje de consulta de introducción toohello utilizado para búsquedas de registros.  Si lo que se pretendía en procesos de hello en otros equipos, puede modificar Hola consulta tooretrieve esa información.

En este caso, podemos ver que proceso de copia de seguridad de hello constantemente consume aproximadamente el 60% de CPU del servidor de aplicaciones de Hola.  Es obvio que este proceso nuevo es responsable de nuestro problema de rendimiento.  Nuestra solución sería obviamente tooremove esta nueva copia de seguridad de software de servidor de aplicaciones de Hola.  Realmente pudimos aprovechamos estado configuración deseado (DSC) administrado por directivas de toodefine de automatización de Azure que se aseguran de que este proceso nunca se ejecuta en estos sistemas críticos.


## <a name="summary-points"></a>Puntos de resumen
- [Service Map](operations-management-suite-service-map.md) le proporciona una vista de toda su aplicación incluso si no conoce todos sus servidores y dependencias.
- Mapa de servicio expone los datos recopilados por otro toohelp de soluciones OMS se identifican los problemas de la aplicación y su infraestructura subyacente.
- [Búsquedas de registro](../log-analytics/log-analytics-log-searches.md) permiten toodrill hacia abajo en datos específicos recopilados en el repositorio de análisis de registros de Hola.    

## <a name="next-steps"></a>Pasos siguientes
- Más información sobre [Service Map](operations-management-suite-service-map.md).
- [Implementación y configuración de Service Map](operations-management-suite-service-map-configure.md).
- Más información sobre [Log Analytics](../log-analytics/log-analytics-overview.md), una aplicación que es necesaria para Service Map y que almacena datos operativos almacenados por los agentes.