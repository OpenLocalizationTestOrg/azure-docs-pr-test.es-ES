---
title: "aaaLogging para servicios web de aprendizaje automático | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable el registro para el aprendizaje automático web services. El registro proporciona información adicional toohelp solucionar Hola API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Habilitar el registro para los servicios web de Aprendizaje automático
Este documento proporciona información sobre Hola registro capacidad de servicios web de aprendizaje automático. El registro proporciona información adicional, más allá de solo un número de error y un mensaje, que puede ayudarle a solucionar problemas de su toohello de llamadas API de aprendizaje de máquina.  

## <a name="how-tooenable-logging-for-a-web-service"></a>¿Cómo registro tooenable para un servicio Web

Para habilitar el registro de hello [servicios Web de Azure Machine Learning](https://services.azureml.net) portal. 

1. Inicie sesión en el portal de servicios Web de Azure Machine Learning toohello en [https://services.azureml.net](https://services.azureml.net). Para un servicio web clásico, también puede obtener toohello portal, haga clic en **nueva experiencia de servicios Web** en la página de servicios Web de aprendizaje de máquina de hello en estudio de aprendizaje automático.

   ![Nuevo vínculo a la experiencia de servicios web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. En la barra de menús superior hello, haga clic en **servicios Web** para un nuevo servicio web o haga clic en **clásico servicios Web** para un clásico de servicio web.

   ![Selección de servicios web nuevos o clásicos](media/machine-learning-web-services-logging/select-web-service.png)

3. Para un nuevo servicio web, haga clic en el nombre del servicio web Hola. Para un servicio web clásico, haga clic en el nombre del servicio web hello y, a continuación, en la página siguiente de hello, haga clic en punto de conexión adecuado de Hola.

4. En la barra de menús superior hello, haga clic en **configurar**.

5. Conjunto hello **Habilitar registro** opción demasiado*Error* (toolog solo errores) o *todos los* (para el registro completo).

   ![Selección del nivel de registro](media/machine-learning-web-services-logging/enable-logging.png)

6. Haga clic en **Guardar**.

7. Para los servicios web estándar, crear hello **ml diagnósticos** contenedor.

   Todos los registros del servicio web se conservan en un contenedor de blobs denominado **ml diagnósticos** en hello cuenta de almacenamiento asociada con el servicio web de Hola. Para los nuevos servicios web, este contenedor se crea Hola primera vez que acceda a servicio web de Hola. Para los servicios web estándar, deberá contenedor de hello toocreate si aún no existe. 

   1. Hola [portal de Azure](https://portal.azure.com), vaya toohello cuenta de almacenamiento asociada con el servicio web de Hola.

   2. En **Blob service**, haga clic en **Contenedores**.

   3. Si el contenedor de hello **diagnósticos de aprendizaje automático** no existe, haga clic en **+ contenedor**, asigne Hola contenedor Hola nombre "ml-diagnostics" y seleccione hello **tipo de acceso** como "Blob". Haga clic en **Aceptar**.

      ![Selección del nivel de registro](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Para un servicio web clásico, Hola panel de servicios Web en estudio de aprendizaje automático también tiene un registro de tooenable de conmutador. Sin embargo, dado que el registro ahora se administra a través del portal de servicios Web de hello, debe tooenable registro a través del portal de hello, tal como se describe en este artículo. Si ha habilitado el registro en Studio, en el Portal de servicios Web de hello, deshabilitar el registro y vuelva a habilitarla.


## <a name="hello-effects-of-enabling-logging"></a>efectos de Hello habilitación del registro
Cuando se habilita el registro, diagnósticos de Hola y errores de extremo de servicio web de Hola se registran en hello **ml diagnósticos** contenedor de blobs en hello cuenta de almacenamiento de Azure vinculado con el área de trabajo del usuario de Hola. Este contenedor contiene toda la información de diagnóstico de Hola para todos los extremos de servicio web de Hola para todas las áreas de trabajo de hello asociadas a esta cuenta de almacenamiento.

Hola registros pueden verse mediante cualquiera de hello tooexplore disponibles de varias herramientas una cuenta de almacenamiento de Azure. Hola más sencilla puede ser toonavigate toohello cuenta de almacenamiento en hello portal de Azure, haga clic en **contenedores**y, a continuación, haga clic en el contenedor de hello **ml diagnósticos**.  

## <a name="log-blob-detail-information"></a>Información detallada sobre el blob de registro
Cada blob en contenedor de hello contiene información de diagnóstico de Hola para exactamente uno de hello siguientes acciones:

* Una ejecución del método hello ejecución por lotes  
* Una ejecución del método hello solicitudes y respuestas  
* Inicialización de un contenedor Request-Response

nombre de Hola de cada blob tiene un prefijo de hello siguiente forma: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Donde _tipo de registro_ es uno de hello siguientes valores:  

* proceso por lotes  
* puntuación/solicitudes  
* puntuación/inic  

