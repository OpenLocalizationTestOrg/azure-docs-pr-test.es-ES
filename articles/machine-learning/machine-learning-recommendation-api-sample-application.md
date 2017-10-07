---
title: "las operaciones de aaaCommon Hola API de recomendaciones de aprendizaje de máquina | Documentos de Microsoft"
description: "Aplicación de ejemplo de recomendación de aprendizaje automático de Azure"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Tutorial de aplicación de ejemplo de la API Recomendaciones
> [!NOTE]
> Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión. Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
> Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Propósito
Este documento muestra el uso de Hola de hello Azure recomendaciones de aprendizaje de máquina API a través de un [aplicación de ejemplo](https://code.msdn.microsoft.com/Recommendations-144df403).

Esta aplicación no está previsto tooinclude toda la funcionalidad ni utiliza Hola todas las API. Muestra algunos tooperform operaciones comunes cuando desee primero tooplay con hello servicio de recomendación de aprendizaje automático. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Introducción tooMachine servicio de recomendación de aprendizaje
Recomendaciones a través de hello servicio de recomendación de aprendizaje automático se habilitan al compilar un modelo de recomendación basado en hello después de datos:

* Un repositorio de elementos de Hola que desea toorecommend, también conocida como un catálogo
* Datos que representa el uso de Hola de elementos por cada usuario o sesión (Esto se puede adquirir con el tiempo a través de la adquisición de datos, no como parte de la aplicación de ejemplo de Hola)

Después de la creación de un modelo de recomendación, se pueden usar elementos de toopredict que un usuario podría estar interesado en, según tooa selecciona de usuario de Hola de conjunto de elementos (o un elemento único).

tooenable Hola escenario anterior, ¿Hola siguiente hello en servicio de recomendación de aprendizaje automático:

* Crear un modelo: se trata de un contenedor lógico que contiene datos de hello (catálogo y uso) y modelos de predicción de Hola. Cada contenedor de modelo se identifica mediante un identificador único que se asigna en el momento de su creación. Este identificador se denomina Id. de modelo de Hola y se utiliza con la mayoría de las API de Hola. 
* Cargar toocatalog: cuando se crea un contenedor del modelo, puede asociar tooit un catálogo.

**Tenga en cuenta**: crear un modelo y cargar tooa catálogo normalmente se realizan una vez para el ciclo de vida de hello modelo.

* Cargar uso: Esto agrega el contenedor del modelo de toohello de datos de uso.
* Crear un modelo de recomendación: una vez haya suficientes datos, puede compilar modelo de recomendación de Hola. Esta operación utiliza toocreate algoritmos de aprendizaje automático superior de hello un modelo de recomendación. Cada compilación está asociada a un identificador único. Deberá tookeep un registro de este identificador porque es necesaria para la funcionalidad de Hola de algunas API.
* Proceso de creación de hello de Monitor: una compilación de modelo de recomendación es una operación asincrónica y puede tardar varias horas de tooseveral minutos, según la cantidad de Hola de datos (catálogo y uso) y Hola parámetros de compilación. Por lo tanto, debe compilación de hello toomonitor. Un modelo de recomendación solo se crea si su compilación asociada finaliza correctamente.
* (Opcional) Elegir una compilación de modelo de recomendación activa: este paso solo es necesario si tiene más de un modelo de recomendación compilado en el contenedor de modelos. Las recomendaciones de tooget solicitud sin indicar el modelo de recomendación active Hola se redirige automáticamente por compilación activa de hello sistema toohello de forma predeterminada. 

**Nota**: los modelos de recomendación activa están listos para su uso en producción y se diseñan para cargas de trabajo de producción. Esto difiere de un modelo de recomendación no activo, que permanece en un entorno similar al de prueba (a veces denominado "de ensayo").

* Obtener recomendación: cuando ya tenga un modelo de recomendación, puede desencadenar recomendaciones para un solo elemento o para una lista de elementos que elija. 

Normalmente, se ejecuta la recomendación Get para un cierto período de tiempo. Durante ese período de tiempo, puede redirigir datos de uso toohello sistema de recomendación de aprendizaje automático, que agrega este contenedor de datos toohello modelo especificado. Cuando haya suficientes datos de uso, puede crear un nuevo modelo de recomendación que incorpore datos de uso adicionales de Hola. 

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2013 o posterior.
* Acceso a Internet 
* Suscripción toohello recomendaciones API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Solución de aplicación de ejemplo de Aprendizaje automático de Azure
Esta solución contiene el código fuente de hello, el uso de ejemplo, archivo de catálogo y paquetes de saludo de toodownload directivas que son necesarios para la compilación.

## <a name="hello-apis-used"></a>Hola API que se usan
aplicación Hello usa la funcionalidad de la recomendación de aprendizaje automático a través de un subconjunto de las API disponibles. Hola que API siguientes se muestran en la aplicación hello:

* Crear modelo: crear un contenedor lógico toohold modelos de datos y la recomendación. Un modelo se identifica mediante un nombre y no se puede crear más de un modelo con hello mismo nombre.
* Cargar archivo de catálogo: utilizar los datos del catálogo de tooupload.
* Cargar archivo de uso: utilizar datos de uso de tooupload.
* Desencadenar la compilación: usar toocreate un modelo de recomendación.
* Supervisar la ejecución de la compilación: usar el estado de hello toomonitor de una compilación de modelo de recomendación.
* Elija un modelo integrado de recomendación: usar tooindicate qué toouse de modelo de recomendación de forma predeterminada para un determinado contenedor del modelo. Este paso es necesario únicamente si tiene más de un modelo de recomendación y desea tooactivate un inactivas compilar como modelo de recomendación active Hola.
* Obtener recomendación: usar tooretrieve elementos según tooa partir del elemento único o un conjunto de elementos recomendado. 

Para obtener una descripción completa de las API de hello, consulte la documentación de Microsoft Azure Marketplace de Hola. 

**Nota**: un modelo puede tener varias compilaciones con el tiempo (no de forma simultánea). Se crea cada compilación con hello igual o un controlador actualizado, catálogo y los datos de uso adicionales.

## <a name="common-pitfalls"></a>Dificultades habituales
* Necesita tooprovide su nombre de usuario y la aplicación de ejemplo de Hola de Microsoft Azure Marketplace cuenta principal toorun clave.
* Aplicación de ejemplo de Hola ejecución consecutivamente se producirá un error. flujo de la aplicación Hello incluye crear, cargar, creación de monitor de Hola y obtener recomendaciones de un modelo predefinido; por lo tanto, generará un error en la ejecución consecutiva si no cambiar el nombre de modelo de hello entre las distintas invocaciones.
* Puede que las recomendaciones no devuelvan datos. aplicación de ejemplo de Hola usa un archivo de catálogo y el uso de muy pequeño. Por lo tanto, algunos elementos de catálogo de hello no tendrá ninguna elementos recomendados.

## <a name="disclaimer"></a>Renuncia de responsabilidades
aplicación de ejemplo de Hola no es toobe previsto ejecutar en un entorno de producción. datos de Hello proporcionados en el catálogo de hello están muy pequeñas y no proporcionará un modelo de recomendación significativo. Hola datos se proporcionan como una demostración. 

