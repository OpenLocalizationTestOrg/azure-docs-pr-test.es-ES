---
title: "información general del proceso de ciencia de datos de equipo aaaAzure | Documentos de Microsoft"
description: "Proporciona un análisis predictivos datos ciencia metodología toodeliver soluciones y aplicaciones inteligentes."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Introducción al proceso de ciencia de datos en equipo

Hola proceso de ciencia de datos de equipo (TDSP) es una herramienta ágil, soluciones de análisis predictivo de datos reiterativos ciencia metodología toodeliver y aplicaciones inteligentes eficazmente. TDSP ayuda a mejorar la colaboración en equipo y el aprendizaje. Contiene una destilación de prácticas recomendadas de Hola y estructuras de Microsoft y otros en el sector de Hola que facilitan la implementación correcta de Hola de las iniciativas de ciencias de datos. objetivo de Hello es toohelp compañías totalmente beneficios Hola de su programa de análisis.

En este artículo se proporciona una introducción a TDSP y sus componentes principales. Proporcionamos una descripción del proceso de hello aquí genérica que se pueden implementar con una variedad de herramientas. Se proporciona una descripción más detallada de las tareas de proyecto de Hola y roles implicados en el ciclo de vida de Hola de proceso de hello en otros temas vinculados. Instrucciones sobre cómo se proporciona también tooimplement hello TDSP con un conjunto específico de infraestructura que utilizamos tooimplement hello TDSP en nuestros equipos y herramientas de Microsoft.

## <a name="key-components-of-hello-tdsp"></a>Componentes clave de hello TDSP

TDSP consta de hello clave de los componentes siguientes:

- Una definición de **ciclo de vida de ciencia de datos**
- Una **estructura de proyecto estandarizada**
- **Infraestructura y recursos** para proyectos de ciencia de datos
- **Herramientas y utilidades** para la ejecución de proyectos


## <a name="data-science-lifecycle"></a>Ciclo de vida de ciencia de datos

Hola proceso de ciencia de datos de equipo (TDSP) proporciona un desarrollo de hello toostructure de ciclo de vida de los proyectos de ciencia de datos. ciclo de vida de Hello describe los pasos de hello, de toofinish de inicio, que los proyectos suelen seguir cuando se ejecutan.

Si está usando otro ciclo de vida de ciencia de datos, como [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) o el proceso personalizado de la organización, puede seguir usando Hola TDSP basado en tareas en el contexto de Hola de esos desarrollo ciclos de vida. En un nivel alto, estas distintas metodologías tienen mucho en común. 

Este ciclo de vida se ha diseñado para proyectos de ciencia de datos que se enviarán como parte de aplicaciones inteligentes. Estas aplicaciones implementan modelos de aprendizaje o inteligencia artificial de máquina para realizar un análisis predictivo. Los proyectos de ciencia de datos exploratorios o proyectos de análisis ad hoc también se pueden beneficiar del uso de este proceso. Pero en estos casos algunos de los pasos de hello descritos no es necesario.    

ciclo de vida de Hello TDSP se compone de cinco fases principales que se ejecutan de forma iterativa:

* **Conocimiento del negocio**
* **Adquisición y comprensión de los datos**
* **Modelado**
* **Implementación**
* **Aceptación del cliente**

Esta es una representación visual de hello **ciclo de vida del proceso de ciencia de datos de equipo**. 

![Ciclo de vida de TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Hello objetivos, tareas y artefactos de la documentación de cada fase del ciclo de vida de hello en TDSP se describen en hello [ciclo de vida del proceso de ciencia de datos de equipo](data-science-process-lifecycle.md) tema. Estas tareas y artefactos están asociados con roles de proyecto:

- Arquitecto de soluciones
- Jefe de proyecto
- Científico de datos
- Responsable de proyecto 

Hello siguiente diagrama proporciona una vista de cuadrícula de tareas de hello (en azul) y artefactos (en verde) asociados a cada fase del ciclo de vida de hello (en el eje horizontal de hello) para estos roles (en el eje vertical de hello). 

![Roles y tareas de TDSP](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Estructura de proyecto estandarizada

Cuando todos los proyectos comparten una estructura de directorios y utilizar plantillas de documentos del proyecto, resulta fácil para obtener información de miembros toofind equipo de hello sobre sus proyectos. Todo el código y documentos se almacenan en un sistema de control de versiones (VCS) como Git, TFS o Subversion tooenable colaboración en equipo. El seguimiento de las tareas y características en un sistema, como Jira de seguimiento de proyectos ágiles, Rally, Visual Studio Team Services permite más cerca de seguimiento de código de hello de cada característica. Este seguimiento también permite mejorar las estimaciones de costes de tooobtain de los equipos. TDSP recomienda crear un repositorio independiente para cada proyecto en hello VCS para colaboración, seguridad de la información y control de versiones. Hola estandarizados estructura para todos los proyectos ayuda a generar institucional conocimiento a través de la organización de Hola.

Se proporcionan plantillas para la estructura de carpetas de Hola y documentos necesarios en las ubicaciones estándar. Esta estructura de carpetas organiza los archivos de Hola que contiene código para la exploración de datos y extracción de características y que registre iteraciones de modelo. Estas plantillas que sea más fácil para el trabajo de toounderstand de los miembros de equipo realizado por otros usuarios y tooadd nuevos miembros tooteams. Es fácil plantillas de documento tooview y update en formato de marcado. Usar listas de comprobación de plantillas tooprovide con preguntas clave para cada tooinsure de proyecto que problema Hola está bien definido y ese entregas cumplan calidad Hola se esperaba. Algunos ejemplos son:

- un problema empresarial de proyecto carta toodocument Hola y el ámbito del proyecto de Hola
- estructura de datos de informes toodocument hello y las estadísticas de los datos sin procesar de Hola
- Hola de modelo informes toodocument derivada características
- métricas de rendimiento de modelo, como curvas ROC o MSE


![Directorios de TDSP](./media/data-science-process-overview/tdsp-dir-structure.png)

se puede clonar la estructura de directorios de Hola de [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infraestructura y recursos para los proyectos de ciencia de datos

TDSP proporciona recomendaciones para administrar análisis compartido e infraestructura de almacenamiento, por ejemplo:

- sistemas de archivos en la nube para almacenar conjuntos de datos 
- bases de datos
- clústeres de macrodatos (Hadoop o Spark) 
- servicios de aprendizaje automático. 

infraestructura de almacenamiento y análisis de Hola puede estar en la nube Hola o de forma local. Aquí es donde se almacenan los conjuntos de datos sin procesar y procesados. Esta infraestructura permite un análisis reproducible. También evita la duplicación, lo cual puede conducir tooinconsistencies y los costos de infraestructura innecesaria. Las herramientas son siempre tooprovision Hola recursos compartidos, seguirlos y permitir que cada tooconnect de miembro de equipo toothose recursos forma segura. También es una buena práctica pedir a los miembros del proyecto que creen un entorno de proceso coherente. Luego, diferentes miembros del equipo pueden replicar y validar los experimentos.

Este es un ejemplo de un equipo que trabaja en varios proyectos y que comparte diversos componentes de la infraestructura de análisis.

![Infraestructura de TDSP](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Herramientas y utilidades para la ejecución de proyectos

En la mayoría de las organizaciones la introducción de procesos presenta ciertos desafíos. Se proporcionan herramientas de ciclo de vida y el proceso de ciencia de datos de tooimplement Hola ayudan inferior Hola barreras tooand aumentar la coherencia de Hola de su adopción. TDSP proporciona un conjunto inicial de herramientas y scripts de inicio toojump la adopción de TDSP dentro de un equipo. También ayuda a automatizar algunas tareas comunes de hello en hello ciclo de vida de ciencia de datos, como exploración de datos y modelado de línea de base. Hay una estructura bien definida proporcionados para usuarios toocontribute había compartido herramientas y utilidades en el repositorio de código compartido de su equipo. A continuación, se pueden aprovechar estos recursos por otros proyectos de equipo de hello u organización de Hola. TDSP también planea las contribuciones de hello tooenable de herramientas y utilidades toohello conjunto de la Comunidad. Utilidades de Hello TDSP pueden clonarse de [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Pasos siguientes

[Proceso de ciencia de datos de equipo: Los Roles y tareas](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) se describen los roles del personal clave hello y sus tareas asociadas para un equipo de ciencia de datos que normaliza en este proceso. 
