---
title: "aaaOptimize del entorno de Active Directory con análisis de registros de Azure | Documentos de Microsoft"
description: "Puede usar Hola Active evaluación Directory solución tooassess Hola a riesgo y el estado de los entornos de servidor a intervalos regulares."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Optimizar el entorno de Active Directory con hello solución de evaluación de Active Directory en el análisis de registros

![Símbolo de AD Assessment](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Puede usar Hola Active evaluación Directory solución tooassess Hola a riesgo y el estado de los entornos de servidor a intervalos regulares. En este artículo le ayuda a instalar y usar la solución de Hola para que pueda tomar medidas correctivas para detectar posibles problemas.

Esta solución proporciona una lista de prioridades de infraestructura de servidor implementada tooyour específico de recomendaciones. recomendaciones de Hola se clasifican en foco cuatro áreas que le ayudarán a rápidamente comprender Hola a riesgo y tome las medidas.

Hola recomendaciones se basan en los conocimientos de Hola y experiencias adquiridas por los ingenieros de Microsoft de miles de visitas de clientes. Cada recomendación proporcionan instrucciones acerca de por qué un problema podría ser importante tooyou y cómo tooimplement Hola sugiere cambios.

Puede elegir las áreas de enfoque que son más importante organización tooyour y realizar un seguimiento del progreso hacia la consecución de un entorno de riesgo libre y en buen estado.

Después de que haya agregado la solución de Hola y una evaluación haya finalizado, resumen se muestra información de las áreas de enfoque en hello **AD evaluación** panel para la infraestructura de hello en su entorno. Hello las secciones siguientes describen cómo toouse Hola información en hello **AD evaluación** panel, donde puede ver y, a continuación, tomar las acciones recomendadas para su infraestructura de servidor de Active Directory.

![imagen del icono de evaluación de SQL](./media/log-analytics-ad-assessment/ad-tile.png)

![imagen del panel de evaluación de SQL](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

* Agentes deben instalarse en controladores de dominio que son miembros de hello dominio toobe evaluada.
* Hola Active evaluación Directory solución requiere una versión compatible de .NET Framework 4 (4.5.2 o posterior) instalado en cada equipo que tenga un agente de OMS.
* Agregar Hola evaluación de Active Directory solución tooyour OMS área de trabajo de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).  No es necesario realizar ninguna configuración más.

  > [!NOTE]
  > Después de Agregar solución hello, archivo de hello AdvisorAssessment.exe se agrega tooservers con agentes. Datos de configuración se leen y, a continuación, envían toohello servicio OMS en la nube de Hola para su procesamiento. Lógica es aplicado toohello recibe datos y servicio de nube de hello registra datos de Hola.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Detalles de la recopilación de datos para la evaluación de Active Directory

Evaluación de Active Directory recopila datos de hello siguientes orígenes con agentes de Hola que ha habilitado:

- Recopiladores de registros
- Recopiladores de LDAP
- .NET Framework
- Recopiladores de registros de eventos
- Interfaces ADSI
- Windows PowerShell
- Recopiladores de datos de archivo
- Instrumental de administración de Windows (WMI)
- API de la herramienta DCDIAG
- API del servicio de replicación de archivos (NTFRS)
- Código personalizado C#


Hello tabla siguiente muestran los métodos de recopilación de datos para los agentes, si es necesario Operations Manager (SCOM) y cómo se recopilan los datos a menudo por un agente.

| plataforma | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 días |

## <a name="understanding-how-recommendations-are-prioritized"></a>Cómo se establecen prioridades entre las recomendaciones
Cada recomendación efectuada se proporciona un valor de ponderación que identifica Hola importancia relativa de la recomendación de Hola. Se muestran solo recomendaciones más importantes de hello 10.

### <a name="how-weights-are-calculated"></a>Cálculo de las ponderaciones
Las ponderaciones son valores agregados en función de tres factores principales:

* Hola *probabilidad* que un asunto identificado causa problemas. Una probabilidad más alta equivale tooa mayor puntuación total de recomendación de Hola.
* Hola *impacto* de problema de hello en su organización en caso de que se produzca un problema. Un mayor impacto equivale tooa mayor puntuación total de recomendación de Hola.
* Hola *esfuerzo* necesario recomendación de hello tooimplement. Un mayor esfuerzo equivale tooa de puntuación total menor para la recomendación de Hola.

Hola ponderación de cada recomendación se expresa como un porcentaje de hello puntuación total disponible para cada área de enfoque. Por ejemplo, si una recomendación de seguridad de Hola y de área de enfoque de cumplimiento tiene una puntuación del 5%, implementación de esa recomendación aumenta la seguridad y cumplimiento de normas puntuación total por 5%.

### <a name="focus-areas"></a>Áreas de enfoque
**Seguridad y cumplimiento** : este apartado muestra recomendaciones en caso de posibles amenazas e infracciones de seguridad, directivas corporativas y requisitos de cumplimiento técnico, legal y reglamentario.

**Disponibilidad y continuidad empresarial** : este apartado muestra recomendaciones relacionadas con la disponibilidad de servicio, la resistencia de la infraestructura y la protección del negocio.

**Rendimiento y escalabilidad** -esta área de enfoque muestra toohelp recomendaciones de su organización crecer de infraestructura de TI, asegúrese de que su entorno de TI cumple los requisitos de rendimiento actuales y es capaz de toorespond toochanging necesidades de infraestructura.

**Actualización, migración e implementación** : toohelp recomendaciones actualizar muestra esta área de enfoque, migración e implementar la infraestructura existente de Active Directory tooyour.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>¿Debe conseguir tooscore 100% en cada área de enfoque?
No necesariamente. Hola recomendaciones se basan en los conocimientos de Hola y las experiencias adquiridas por los ingenieros de Microsoft fruto de miles de visitas de clientes. Sin embargo, no hay dos infraestructuras de servidores son Hola igual y determinadas recomendaciones puedan ser tooyou más o menos relevante. Por ejemplo, algunas recomendaciones de seguridad pueden ser menos relevantes si las máquinas virtuales no están expuesto toohello Internet. Algunas recomendaciones de disponibilidad pueden ser menos relevantes para los servicios que proporcionan informes y recopilaciones de datos ad hoc de baja prioridad. Los problemas que son tooa importante para el negocio maduro pueden inicio de tooa menos importante. Puede desea tooidentify qué áreas de enfoque son prioritarias para usted y, a continuación, observar cómo cambian las puntuaciones con el tiempo.

Cada recomendación incluye pautas que indican por qué es importante. Debe usar esta guía tooevaluate si implementa la recomendación de hello es adecuado para usted, dada la naturaleza de Hola de sus necesidades de negocio de hello y servicios de TI de su organización.

## <a name="use-assessment-focus-area-recommendations"></a>Uso de las recomendaciones de área de enfoque de evaluación
Antes de poder usar una solución de evaluación en OMS, debe tener instalada la solución de Hola. tooread más acerca de cómo instalar soluciones, consulte [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). Después de instalarlo, puede ver resumen de Hola de recomendaciones mediante el icono de evaluación de hello en la página de información general de Hola de OMS.

Hola de vista resume de las evaluaciones de cumplimiento para su infraestructura y, a continuación, profundizar en recomendaciones.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendaciones de tooview para una acción correctora foco área y take
1. En hello **Introducción** página, haga clic en hello **evaluación** icono para su infraestructura de servidor.
2. En hello **evaluación** página, revise la información de resumen de hello en uno de los módulos de área de enfoque de hello y, a continuación, haga clic en uno tooview recomendaciones para dicha área de enfoque.
3. En cualquiera de las páginas de área de enfoque de hello, puede ver recomendaciones de hello prioridad diseñadas para su entorno. Haga clic en una recomendación en **objetos afectados** tooview detalles sobre por qué se realiza la recomendación de Hola.  
    ![imagen de las recomendaciones de evaluación](./media/log-analytics-ad-assessment/ad-focus.png)
4. Puede tomar las medidas correctivas que se sugieren en **Acciones sugeridas**. Cuando se haya tratado elemento hello, los registros de las evaluaciones posteriores que recomienda acciones se han realizado y aumentará su calificación de cumplimiento de normas. Los asuntos que se hayan corregido aparecerán en **Objetos superados**.

## <a name="ignore-recommendations"></a>Omisión de las recomendaciones
Si tiene las recomendaciones que desea tooignore, puede crear un archivo de texto que utilice OMS tooprevent recomendaciones que aparecen en los resultados de la evaluación.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendaciones de tooidentify que pasarán por alto
1. Inicie sesión en el área de trabajo de tooyour y abra búsqueda de registros. Usar hello siguiendo las recomendaciones de toolist de consultas con error para los equipos de su entorno.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Esta es una consulta de búsqueda de registros de captura de pantalla mostrando hello: ![no se pudo recomendaciones](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Elija las recomendaciones que desea tooignore. Usará los valores de hello de RecommendationId en el procedimiento siguiente Hola.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate y usar un archivo de texto IgnoreRecommendations.txt
1. Cree un archivo llamado IgnoreRecommendations.txt.
2. Pegue o escriba cada valor de RecommendationId para cada recomendación desea tooignore de análisis de registros en una línea independiente y, a continuación, guarde y cierre el archivo hello.
3. Coloque el archivo de Hola Hola después de carpeta en cada equipo donde desea que las recomendaciones de tooignore OMS.
   * En equipos con Microsoft Monitoring Agent (conectado directamente o a través de Operations Manager): hello *SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * En el servidor de administración de Operations Manager de hello - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que se omiten las recomendaciones
Después de hello próxima evaluación programada se ejecuta de forma predeterminada cada 7 días, Hola especificado se marcan recomendaciones *omitido* y no aparecerán en el panel de evaluación de Hola.

1. Puede usar Hola después a toolist de las consultas de búsqueda de registros todas las recomendaciones de hello pasa por alto.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Si más adelante decide que desea que las recomendaciones de toosee pasa por alto, quite todos los archivos IgnoreRecommendations.txt o quite los valores de Recommendationid de ellos.

## <a name="ad-assessment-solutions-faq"></a>Preguntas más frecuentes sobre las soluciones de evaluación de AD
*¿Con qué frecuencia se ejecuta una evaluación?*

* evaluación de Hola se realiza cada 7 días.

*¿Cuál es la frecuencia con un tooconfigure manera Hola evaluación se realiza?*

* De momento, no.

*Si se detecta otro servidor después de haber agregado una solución de evaluación, ¿se evaluará?*

* Sí, una vez que se detecte, se evaluará cada 7 días a partir de entonces.

*¿Si se retira un servidor, cuándo se quitará de evaluación de hello?*

* Si un servidor no envía datos durante 3 semanas, se quitará.

*¿Cuál es el nombre de hello del proceso de Hola que Hola la recopilación de datos?*

* AdvisorAssessment.exe

*¿Cuánto tarda para toobe de datos que se recopilan?*

* recopilación de datos reales de Hello en servidor hello tarda aproximadamente 1 hora. Puede demorar más en servidores que tengan una gran cantidad de servidores de Active Directory.

*¿Hay una manera tooconfigure cuando los datos se recopilan?*

* De momento, no.

*¿Por qué se muestran solo Hola 10 recomendaciones principales?*

* En lugar de darle una lista exhaustiva y abrumadora de tareas, se recomienda centrarse primero en un nivel de prioridad de hello recomendaciones. Después de aplicarlas, se mostrarán más recomendaciones. Si lo prefiere lista detallada de toosee hello, puede ver todas las recomendaciones mediante la búsqueda de registros.

*¿Hay una manera tooignore una recomendación?*

* Sí, consulte la sección [Omisión de las recomendaciones](#ignore-recommendations) anterior.

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de la evaluación de AD y recomendaciones.
