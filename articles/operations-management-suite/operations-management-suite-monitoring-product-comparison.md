---
title: "aaaMicrosoft supervisión comparación del producto | Documentos de Microsoft"
description: "Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local.  En este artículo se identifican Hola servicios diferentes incluidos en OMS y se proporcionan vínculos tootheir detallada contenido."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Comparación de productos de supervisión de Microsoft
Este artículo proporciona una comparación entre System Center Operations Manager (SCOM) y análisis de registros de Operations Management Suite (OMS) en cuanto a su arquitectura, la lógica de Hola de cómo supervisar los recursos y cómo funcionan el análisis de datos de Hola recopilar.  Se trata de toogive que unos conocimientos básicos sobre de sus diferencias y capacidades relativas.  

## <a name="basic-architecture"></a>Arquitectura básica
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Todos los componentes de SCOM están instalados en su centro de datos.  [Los agentes están instalados](http://technet.microsoft.com/library/hh551142.aspx) en equipos Windows y Linux administrados por SCOM.  Agentes se conectan demasiado[servidores de administración](https://technet.microsoft.com/library/hh301922.aspx) que comunicarse con el almacenamiento de base de datos y los datos SCOM Hola.  Los agentes se basan en los servidores de dominio de autenticación tooconnect toomanagement.  Aquellos fuera de un dominio de confianza pueden realizar la autenticación de certificado o conectar tooa [servidor de puerta de enlace](https://technet.microsoft.com/library/hh212823.aspx).

SCOM requiere dos bases de datos SQL, uno para los datos operativos y otro almacenamiento toosupport informes y datos de análisis de datos.  A [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) ejecuta tooreport de SQL Reporting Services en los datos de almacenamiento de datos de Hola. 

SCOM puede supervisar los recursos en la nube con los módulos de administración para productos como [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708) y [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Estos módulos de administración usan uno o más agentes locales como servidores proxy para la detección de recursos y ejecutar flujos de trabajo toomeasure su rendimiento y disponibilidad en la nube.  Los agentes proxy también se usan demasiado[supervisar dispositivos de red](https://technet.microsoft.com/library/hh212935.aspx) y otros recursos externos.

Hello consola del operador es una aplicación de Windows que se conecta tooone Hola de servidores de administración y permite Hola administrador tooview y analizar los datos recopilados y configura el entorno de SCOM Hola.  Una consola basada en web se puede hospedar en cualquier servidor IIS y proporciona análisis de datos a través de un explorador.

![Arquitectura de SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
La mayoría de los componentes de OMS son Hola nube de Azure para que pueda implementar y administrar con un costo mínimo y el esfuerzo administrativo.  Todos los datos recopilados por el análisis de registro se almacena en el repositorio OMS Hola.

Log Analytics puede recopilar datos desde uno de estos tres orígenes:

* Máquinas físicas y virtuales con Windows hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) o hello y Linux [agente de Operations Management Suite para Linux](https://technet.microsoft.com/library/mt622052.aspx).  Estos equipos pueden ser locales o máquinas virtuales en Azure u otra nube.
* Una cuenta de Almacenamiento de Azure con datos de [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) que recopila datos de un rol de trabajo de Azure, rol web o máquina virtual.
* [Grupo de administración de SCOM de conexión tooa](https://technet.microsoft.com/library/mt484104.aspx).  En esta configuración, los agentes de Hola se comunican con los servidores de administración de SCOM lo que reporta una base de datos SCOM de hello datos toohello dónde se entregó, a continuación, almacén de datos OMS toohello.
  Los administradores analizar los datos recopilados y configurar análisis de registros con el portal de OMS de Hola que se hospeda en Azure y puede tener acceso desde cualquier explorador.  Aplicaciones móviles tooaccess estos datos están disponibles para plataformas de hello estándar.

![Arquitectura de Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integración de SCOM y Log Analytics
Cuando SCOM se utiliza como origen de datos para análisis de registros, puede aprovechar características de Hola de ambos productos en un entorno de supervisión de híbrido.  Puede configurar los agentes SCOM existentes a través de toobe de la consola del operador de hello administrados por OMS, además de módulos de administración de toorun toocontinuing de SCOM.  
Los datos de un grupo de administración de SCOM conectado se entregan tooLog análisis mediante uno de los cuatro métodos:

* Eventos y datos de rendimiento se recopilan por el agente de Hola y entregan tooSCOM.  Servidores de administración de SCOM, a continuación, entregar Hola datos tooLog análisis.
* Algunos eventos, como los registros IIS y eventos de seguridad continúan toobe entreguen tooLog análisis directamente desde el agente de Hola.
* Algunas soluciones se entregar a agente toohello de software adicional o requiere que el software sea datos adicionales toocollect instalado.  Estos datos normalmente se enviará directamente tooLog análisis.
* Algunas soluciones recopilará datos directamente desde los servidores de administración de SCOM que no proceden de agente de Hola.  Por ejemplo, hello [solución de administración de alertas](https://technet.microsoft.com/library/mt484092.aspx) recopila alertas de SCOM después de que se hayan creado.

## <a name="monitoring-logic"></a>Lógica de supervisión
SCOM y análisis de registros funcionan con datos similares procedentes de agentes pero tienen diferencias fundamentales en cómo definen e implementan la lógica para la recopilación de datos y cómo analizar los datos Hola que recopilan.

### <a name="operations-manager"></a>Operations Manager
Lógica de la supervisión de SCOM se implementa en [módulos de administración](https://technet.microsoft.com/library/hh457558.aspx) que contienen lógica para la detección de componentes toomonitor, medir el estado de Hola de dichos componentes y para recopilar datos tooanalyze.  La supervisión de datos puede ser tan simple como la recopilación de un evento o contador de rendimiento, o podría usar la lógica compleja que se implementa en un script.  Módulos de administración que incluyen supervisión completa están disponibles para una amplia variedad de [aplicaciones de Microsoft y terceros](http://go.microsoft.com/fwlink/?LinkId=82105) en suma toohardware y dispositivos de red.  También puede [crear sus propios módulos de administración](http://aka.ms/mpauthor) para aplicaciones personalizadas.

Módulos de administración contienen varios flujos de trabajo que realizan algunas funciones de supervisión distintos, como un contador de rendimiento de muestreo, comprobando el estado de saludo de un servicio o ejecutar un script.  Cada flujo de trabajo se ejecuta de forma independiente y define sus propios resultados como base de datos que se escribirá tooand si generará una alerta. 

Puede invalidar los detalles del flujo de trabajo como la frecuencia de Hola que se ejecuten, donde considera un error de umbral de Hola y Hola gravedad de alerta de Hola que generan.  También puede proporcionar una funcionalidad adicional mediante la adición de sus propios flujos de trabajo.

![Invalidaciones](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Módulos de administración se instalan en la base de datos de Operations Manager de Hola y distribuyen automáticamente tooagents servidores de administración.  Descargar módulos de administración y de carga de aplicaciones de toohello relevantes de los flujos de trabajo que ha instalado automáticamente cada agente.  Datos recopilados por el agente de Hola se entregan a toohello espera el servidor de administración para la inserción en el almacén de datos y la base de datos SCOM Hola.  Hola consola del operador permite tooview y analizar estos datos a través de vistas personalizadas, paneles e informes que se incluye en el módulo de administración de Hola.

distribución de Hola de módulos de administración se muestra en hello siguiente diagrama.

![Flujo del módulo de administración](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Recopilación de rendimiento y eventos
Log Analytics recopila eventos y contadores de rendimiento de los sistemas de agente con orígenes como el registro de eventos de Windows, los registros de IIS y Syslog.  Puede definir criterios para que los datos se recopilan a través del portal de análisis de registros de hello y, a continuación, crear consultas de registros tooanalyze Hola recopilan datos.  Un conjunto de criterios estándar se define cuando se crea el área de trabajo de OMS, y puede definir datos adicionales para aplicaciones concretas. 

![Definición de registros de eventos en Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Aunque SCOM tiene muchos flujos de trabajo detallados que normalmente definen criterios específicos para los datos y acción de Hola que debe realizarse en respuesta, análisis de registros tiene criterios más generales para la recopilación de datos.  Las consultas de registros y soluciones proporcionan más criterios de destino para analizar y actuar en datos específicos en la nube de hello después de que se han recopilado.

#### <a name="solutions"></a>Soluciones
Las soluciones proporcionan una lógica adicional para el análisis y la recopilación de datos.  Puede seleccionar suscripción de OMS de soluciones tooadd tooyour de hello Galería de soluciones.

![Galería de soluciones](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Principalmente ejecutan soluciones en nube Hola proporciona un análisis de eventos y contadores de rendimiento recopilados en el repositorio OMS Hola.  También pueden definir recopilan toobe de datos adicionales que se pueden analizar con consultas de registros o mediante la interfaz de usuario adicionales de solución de hello en el panel de OMS de Hola. 

Por ejemplo, hello [solución de seguimiento de cambios](https://technet.microsoft.com/library/mt484099.aspx) detecta configuración cambios en los sistemas de agente y escribe eventos toohello OMS detectado de repositorio que se pueden analizar con varias vistas gráficas que resuman los cambios.  Puede explorar en profundidad desde la vista de resumen de hello en consultas de registro que Hola de mostrar los datos recopilados por solución Hola detallados.

Aunque puede seleccionar qué soluciones Agregar suscripción tooyour, actualmente no tiene Hola capacidad toocreate sus propias soluciones.  Puede seleccionar los eventos de Hola y toocollect de contadores de rendimiento y crear vistas personalizadas en función de sus propias consultas de registro.

Hola lógica de supervisión para el análisis de registros se resume en hello siguiente diagrama.

![Flujo de soluciones de Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Supervisión del estado
### <a name="operations-manager"></a>Operations Manager
SCOM puede modelar Hola diferentes componentes de una aplicación y proporcionar un estado en tiempo real de cada uno de ellos.  Esto permite toonot solo vista detectó errores y rendimiento en el tiempo, pero también toovalidate Hola estado real de una aplicación o del sistema y cada uno de sus componentes en un momento dado.  Porque comprende Hola períodos de tiempo que una aplicación está disponible, el motor de mantenimiento de hello en SCOM también admite contratos de nivel de servicio (SLA) que analizar e informar sobre la disponibilidad de Hola de una aplicación con el tiempo.

Por ejemplo, vista de hello siguiente muestra estado en tiempo real de Hola de motores de base de datos SQL supervisado por SCOM.  estado de Hola de cada una de las bases de datos de Hola para uno de los motores de base de datos de Hola se muestra en la parte inferior de Hola la mitad de la vista de Hola.

![Vista de estado](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Hola Explorador de estado de uno de los motores de base de datos de Hola se muestra a continuación con monitores con hello toodetermine usado su estado general.  Estos monitores se definen en hello módulo de administración de SQL y se ejecutarán todos los motores de base de datos SQL detectados por SCOM.

![Explorador de estado](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Componentes en varios sistemas pueden ser toomeasure combinado Hola mantenimiento de una aplicación distribuida.  Esto puede ser especialmente útil para aplicaciones de línea de negocio que incluyan varios componentes distribuidos.  Puede crear un modelo que mide Hola estado de cada componente de ese paquete acumulativo de actualizaciones en la disponibilidad de la aplicación hello.

Active Directory es un ejemplo de un módulo de administración que proporciona un modelo tooanalyze sus componentes distribuidos.  diagrama de ejemplo de Hola a continuación se muestra en estado de Hola de Hola entorno general y la relación de hello entre bosques, dominios y controladores de dominio.  Cada uno de estos componentes incluyen subcomponentes y varios monitores similar ejemplo SQL toohello anterior.

![Vista de diagrama de SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS no incluyen un aplicaciones comunes de toomodel motor o medir su estado en tiempo real.  Las soluciones individuales pueden evaluar Hola estado general de determinados servicios en función de los datos recopilados y puede instalar lógica personalizada en el análisis en tiempo real de hello agente tooperform.  Dado que las soluciones que se ejecutan en la nube de hello con el repositorio de OMS de toohello de acceso, a menudo pueden ofrecer un análisis más profundo que normalmente se realiza por módulos de administración. 

Por ejemplo, hello [soluciones de evaluación de AD y evaluación de SQL](https://technet.microsoft.com/library/mt484102.aspx) analizar los datos recopilados y proporcionar una clasificación para los distintos aspectos del entorno de Hola.  Incluye recomendaciones para mejoras que pueden realizarse disponibilidad de hello tooimprove y el rendimiento del entorno de Hola.

![Solución de evaluación de AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Análisis de datos
SCOM y análisis de registros proporcionan diversas características tooanalyze recopilan datos.  SCOM tiene vistas y paneles en la consola del operador de Hola para analizar los datos recientes en una variedad de formatos y los informes para presentar datos de almacenamiento de datos de hello en formato tabular.  Análisis de registros proporciona una interfaz y el lenguaje de consulta de registro completo para analizar los datos en el repositorio OMS Hola.  Cuando SCOM se utiliza como origen de datos para análisis de registros, repositorio de hello incluye datos recopilados por SCOM para que herramientas de análisis de registros de hello pueden ser datos de uso tooanalyze desde ambos sistemas.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Vistas
Las vistas en la consola del operador de hello permiten que tooview diferentes tipos de datos recopilados por SCOM en formatos diferentes, normalmente tabulares de eventos, alertas y datos de estado y los gráficos de líneas para los datos de rendimiento.  Vistas de realizan análisis mínimo o consolidación de datos de hello pero permitir toofilter según criterios de tooparticular. 

![Vistas](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Módulos de administración normalmente ofrecerán varias vistas de compatibilidad con la aplicación hello o sistema que supervisa.  Esto puede incluir vistas de estado para objetos distintos de Hola que detecta el módulo de administración de hello, vistas de alerta para los problemas detectados y las vistas de rendimiento para los contadores.

Las vistas son especialmente adecuadas para el análisis del estado actual de hello del entorno de hello incluidos alertas abiertas y el estado de mantenimiento de Hola de sistemas supervisados y objetos.  Puede explorar en profundidad datos de evento o rendimiento toodetailed admitir una alerta determinada en orden toodiagnose su causa. De forma similar, puede ver el rendimiento de Hola y el estado de diferentes componentes de una aplicación tooassess su estado actual.

#### <a name="dashboards"></a>Paneles
Paneles en hello consola del operador trabajan principalmente con Hola mismos datos como vistas pero son más personalizables y pueden incluir visualizaciones más ricas.  Hay disponible un conjunto de paneles estándar que puede personalizar con facilidad para sus propios fines.  También puede utilizar un widget de PowerShell que puede mostrar los datos devueltos de una consulta de PowerShell.

![Panel](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Los desarrolladores tienen Hola capacidad tooadd componentes personalizados toodashboards incluyen en sus módulos de administración.  Esto puede ser muy especializada tooa aplicación concreta como panel de Hola Hola módulo de administración de SQL se muestra a continuación.  Este panel también puede utilizarse como plantilla para versiones personalizadas.

![Panel SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Informes
Informes en SCOM analizar los datos de almacenamiento de datos de hello en formato tabular.  Pueden imprimirse y programarse para la entrega automatizada en diferentes formatos de archivo como PDF, CSV y Word.  Los informes funcionan con datos de almacenamiento de datos de Hola para que sean especialmente adecuados para el análisis de tendencias a largo plazo.

Normalmente, los módulos de administración proporcionarán informes personalizados para una aplicación determinada.  También puede realizar la selección a partir de una biblioteca de informes genéricos que puede personalizar para sus propias aplicaciones o para llevar a cabo un análisis ad hoc.

Aquí te mostramos un informe de rendimiento de ejemplo que muestra los datos recopilados por hello Active Directory Management Pack.

![Informe](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Análisis de registro tiene una [lenguaje de consulta](https://technet.microsoft.com/library/mt484120.aspx) que puede utilizar analysis tooperform en datos desde varias aplicaciones sin Hola necesidad toocreate una vista personalizada o un informe.  Dado que OMS se implementa en la nube de hello, rendimiento de las consultas y análisis de datos no son limitaciones del hardware tooany asunto y puede analizar rápidamente las consultas incluidas millones de registros. 

Las consultas de análisis de registros también son base Hola de otras funcionalidades.  Puede guardar una consulta, exportar su tooExcel resultados o que se ejecute a intervalos regulares automáticamente y generar una alerta si los resultados coinciden con criterios concretos.  

![Flujo de consulta de registro](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

A continuación se muestra un ejemplo de una consulta de Log Analytics.  En este ejemplo se devuelven todos los eventos con "iniciado" en nombre de Hola y se agrupados por el evento Id.  usuario Hola simplemente proporciona consultas de Hola y análisis de registros genera dinámicamente el análisis del Hola Hola usuario interfaz tooperform.  Al seleccionar cualquier elemento de lista de Hola devolverá Hola obtener datos del evento.

![Consulta de registro](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Además tooproviding análisis ad hoc, las consultas de análisis de registros pueden guardarse para uso futuro y también ha agregado tooyour [panel de OMS](http://technet.microsoft.com/library/mt484090.aspx) tal y como se muestra en el siguiente ejemplo de Hola.

![panel de OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Pasos siguientes
* Implemente [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Suscríbase a [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics).  

