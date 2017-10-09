---
title: "administración de aaaAlert en productos de supervisión de Microsoft | Documentos de Microsoft"
description: "Una alerta indica un problema que requiere la atención por parte del administrador.  Este artículo describe las diferencias de hello en cómo se crean y administran en System Center Operations Manager (SCOM) y análisis de registros de alertas y proporciona mejores prácticas para aprovechar los dos productos de Hola para una estrategia de administración de alertas híbrida."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Administración de alertas con la supervisión de Microsoft
Una alerta indica un problema que requiere la atención por parte del administrador.  Hay claras diferencias entre System Center Operations Manager (SCOM) y Log Analytics en Operations Management Suite (OMS) en cuanto a cómo se crean alertas, cómo se administran y analizan, y cómo se notifica que se ha detectado un problema crítico.

## <a name="alerts-in-operations-manager"></a>Alertas en Operations Manager
Se generan alertas en SCOM por reglas individuales o monitores tooindicate un problema específico.  Un monitor puede generar una alerta cuando entra en un estado de error, mientras que una regla puede generar una alerta tooindicate algún problema crítico que no sea toohello directamente relacionada con el estado de un objeto administrado.  Módulos de administración incluyen una variedad de flujos de trabajo creados por las alertas de aplicación Hola o servicio que administran.  Parte del proceso de Hola de configurar un nuevo módulo de administración está optimizando tooensure que no recibirá alertas excesivas para problemas que no considere críticos.

![Vista de alertas de SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM proporciona administración completa de alertas con las alertas que tiene un estado que los administradores pueden cambiar mientras trabajan problema de hello tooresolve.  Cuando se ha resuelto el problema de Hola, Administrador de Hola establece hello tooclosed alerta en ese momento ya no aparecerá en las vistas de mostrar las alertas activas.  Las alertas que se generan a partir de los monitores pueden resolverse automáticamente al monitor de hello devuelve tooa de estado correcto.

![Estado de alerta](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Alertas de Log Analytics
Se crea una alerta en Log Analytics desde una consulta de registro que se ejecuta automáticamente en intervalos regulares.  Puede crear una regla de alerta desde cualquier consulta de registro.  Si consulta Hola devuelve resultados que coinciden con los criterios de Hola que especifique, se crea una alerta.  Podría tratarse de una consulta específica que crea una alerta si se detecta un evento concreto, o puede utilizar una consulta más general que busca cualquier evento de error relacionados con la aplicación en particular tooa.

Alertas de análisis de registro se escriben toohello repositorio de OMS como un evento y se pueden recuperar con una consulta de registro.  No tienen un estado como eventos SCOM por lo que puede indicar si se ha resuelto el problema de Hola.

![Alerta de OMS](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Cuando SCOM se utiliza como origen de datos para análisis de registros, las alertas de SCOM se escriben toohello repositorio de OMS como que se crean y modifican.  

![Alerta de SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Hola [solución de administración de alertas](http://technet.microsoft.com/library/mt484092.aspx) proporciona un resumen de las alertas activas y varias consultas comunes tooretrieve distintos conjuntos de alertas.  Esto le brinda un análisis más eficaz de las alertas que un informe en SCOM.  Puede profundizar en de datos de toodetailed de resúmenes de Hola y crear consultas "ad hoc" tooretrieve distintos conjuntos de alertas.

![solución de administración de alertas](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Notificaciones
Las notificaciones en SCOM enviarán un correo electrónico o texto en tooalerts de respuesta que cumplen determinados criterios.  Puede crear suscripciones de notificación diferentes que tienen distintas personas una notificación según criterios tales como objeto de Hola que se está supervisando, Hola gravedad de alerta de hello, tipo de Hola de problema que ha detectado u Hola hora del día.

Algunas suscripciones pueden ser utilizado tooimplement una estrategia de notificación completa para un gran número de módulos de administración.

![Alertas de SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Log Analytics puede enviarle una notificación por correo electrónico de que se ha creado una alerta mediante el establecimiento de una acción de notificación de correo electrónico en cada [regla de alerta](http://technet.microsoft.com/library/mt614775.aspx).  No tiene capacidad de Hola Hola de SCOM suscribirse toomultiple alertas con una sola regla.  También debe toocreate sus propias reglas de alerta ya no proporcionan OMS cualquier preconfiguradas.

![Alertas de Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Completamente no puede administrar las alertas de SCOM en análisis de registros aunque ya que solo se puede modificar en la consola del operador de Hola.  Log Analytics resulta útil como parte de un proceso de administración de alertas, ya que proporciona herramientas de análisis con las que SCOM no cuenta.

## <a name="alert-remediation"></a>Corrección de alerta
[Corrección](http://technet.microsoft.com/library/mt614775.aspx) hace referencia el problema de hello correcto de tooautomatically tooan intento identificado por una alerta.

SCOM permite toorun diagnósticos y recuperaciones en el monitor de respuesta tooa entra en un estado incorrecto.  Esto sucede a monitor toohello simultáneas crear alerta Hola.  Diagnósticos y recuperaciones normalmente se implementan como una secuencia de comandos que se ejecuta en agente Hola.  Un toogather de intentos de diagnóstico para obtener más información acerca de Hola problema detectado al problema de hello toocorrect de intentos de una recuperación.

Análisis de registros permite toostart una [runbook de automatización de Azure](https://azure.microsoft.com/documentation/services/automation/) o llamar a un webhook de alerta de análisis de registros de tooa de respuesta.  Los runbooks pueden contener una lógica compleja implementada en PowerShell.  script de Hola se ejecuta en Azure y puede tener acceso a los recursos de Azure o recursos externos disponibles de la nube de Hola.  Automatización de Azure tiene Hola capacidad tooexecute runbooks en un servidor en el centro de datos local, pero esta característica no está actualmente disponible al iniciar runbook hello en alertas de respuesta de análisis tooLog.

Los runbooks de OMS y recuperaciones en SCOM puede contener secuencias de comandos de PowerShell, pero las recuperaciones son más difíciles de toocreate y administración, ya que deben estar dentro de un módulo de administración.  Los runbooks se almacenan en Automatización de Azure, que proporciona características para crear, probar y administrar runbooks.

Si usas SCOM como un origen de datos para análisis de registros, puede crear una alerta de análisis de registros mediante un tooretrieve de consulta de registro almacenados en hello repositorio de OMS de alertas de SCOM.  Esto le permitirá toorun un runbook de automatización de Azure en la alerta SCOM tooa de respuesta.  Por supuesto, dado que Hola runbook se ejecutará en Azure, no sería una estrategia viable en las recuperaciones de problemas local.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de los detalles de Hola de [alertas de System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

