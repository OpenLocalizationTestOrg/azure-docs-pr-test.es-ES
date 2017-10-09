---
title: "escenarios comunes de catálogo de datos aaaAzure | Documentos de Microsoft"
description: "Información general de escenarios comunes para el catálogo de datos de Azure, incluido el registro de hello y detección de orígenes de datos de gran valor, la habilitación de inteligencia empresarial de autoservicio y la captura de conocimientos acerca de los orígenes de datos y procesos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Escenarios comunes de Azure Data Catalog
En artículo se muestran escenarios comunes en los que Azure Data Catalog puede ayudar a su organización a obtener más valor de sus orígenes de datos existentes.

## <a name="scenario-1-registration-of-central-data-sources"></a>Escenario 1: registro de orígenes de datos centrales
Las organizaciones suelen tener muchos orígenes de datos de gran valor, entre los que se incluyen la línea de negocio, los sistemas de procesamiento de transacciones en línea (OLTP), el almacenamiento de datos y las bases de datos de análisis e inteligencia empresarial. Hola número de sistemas y Hola se superponen entre ellos, normalmente aumenta con el tiempo según las necesidades empresariales evolucionan y evoluciona de negocio en hello sí a través de, por ejemplo, las fusiones y adquisiciones.

Puede ser difícil para la organización miembros tooknow donde toolocate Hola datos dentro de estos orígenes de datos. Están muy frecuentes preguntas como Hola siguiente:

* ¿Del programa Hola a tres recursos humanos usar sistemas dentro de la empresa de hello, que se debe usar toocreate este tipo de informe?
* ¿Dónde debería ir tooget Hola certificadas las cifras de ventas para el año fiscal Hola que acaba de finalizar?
* ¿Quién debo solicitar o cuál es el proceso Hola debo usar almacenamiento de datos de tooget acceso toohello?
* No sé si estos números son correctos. ¿A quién puedo preguntar para obtener información sobre cómo estos datos se supone toobe usa antes de compartir este panel con mi equipo?

toothese y otras preguntas, catálogo de datos de Azure puede proporcionar respuestas. Hola central, gran valor, orígenes de datos administrada por TI que se usan en las organizaciones a menudo son punto de partida de hello lógica para rellenar el catálogo de Hola. Aunque cualquier usuario puede registrar un origen de datos, con el catálogo de hello kick-started con orígenes de datos de Hola que probablemente tooprovide valor toohello mayor número de usuarios ayuda a impulsar la adopción y uso del sistema de Hola. 

Si comienza a trabajar con el catálogo de datos de Azure, identificar y registrar los orígenes de datos de la clave que se usan por muchos equipos distintos de los consumidores de datos pueden ser el primer toosuccess de paso.

Este escenario presenta también un toomake de orígenes de datos de gran valor de oportunidad tooannotate Hola les sea más fácil toounderstand y acceso. Un aspecto clave de este esfuerzo es tooinclude información sobre cómo los usuarios pueden solicitar el origen de datos de access toohello. Con el catálogo de datos de Azure, puede proporcionar la dirección de correo electrónico de saludo del usuario de Hola o equipo que se encarga de controlar el acceso de origen de datos, herramientas de vínculos tooexisting o documentación o texto sin formato que describe el proceso de solicitud de acceso de Hola. Esta información ayuda a miembros que detectar orígenes de datos registrados pero que aún no dispone de permisos tooaccess Hola tooeasily solicitar acceso de datos mediante el uso de procesos de Hola que se definen y controlan los propietarios de origen de datos de Hola.

## <a name="scenario-2-self-service-business-intelligence"></a>Escenario 2: inteligencia empresarial con características de autoservicio
Aunque las soluciones tradicionales de business intelligence corporativas continuar toobe entornos una parte inestimable de datos de muchas organizaciones, Hola cambiar al ritmo de trabajo ha realizado cada vez más importante BI de autoservicio. Con la inteligencia empresarial con características de autoservicio, tanto las personas que trabajan con información como los analistas pueden crear sus propios informes, libros y paneles sin necesidad de usar un equipo de TI central ni estar restringidos por la programación y disponibilidad de dicho equipo.

En los escenarios de BI con características de autoservicio es habitual que los usuarios combinen datos de varios orígenes, muchos de las cuales puede que no se hayan usado anteriormente para BI y análisis. Aunque algunos de estos orígenes de datos podrían ser conocido, se puede toodiscover un desafío qué toolocate toodo y evaluar los posibles orígenes de datos de una tarea determinada.

Tradicionalmente, este proceso de detección es un manual: los analistas usan su tooidentify de conexiones de red del mismo nivel otras personas que trabajan con datos de Hola que se van a buscar. Después de encontrar y utilizar un origen de datos, Hola proceso se repite nuevo para cada posteriores autoservicio BI esfuerzo, con varios usuarios que realizan un proceso manual redundante de detección.

Con Azure Data Catalog, la organización puede interrumpir este ciclo de esfuerzos. Después de detectar un origen de datos a través de medios tradicionales, un analista puede registrarlo toomake lo más fácilmente reconocible por otros usuarios en hello futuras. Aunque analista Hola puede agregar más valor anotando Hola registrado datos activos, esta anotación no es necesario tootake lugar en hello en el mismo tiempo que el registro. Los usuarios pueden contribuir con el tiempo, como su permiso de programaciones, gradualmente agregar orígenes de datos de valor toohello registrados en el catálogo de Hola.

Este crecimiento orgánica del contenido del catálogo de hello es un registro inicial de toohello complemento natural de los orígenes de datos central. Catálogo de hello previamente rellenar con datos que muchos usuarios necesitan puede ser un factor de motivación para su uso inicial y detección. Habilitar usuarios tooregister y anote orígenes adicionales pueden ser un tookeep de manera actúan de ellos y otros miembros de la organización.

Merece la pena teniendo en cuenta que aunque este escenario se centra específicamente en BI de autoservicio, hello mismo desafíos y patrones se aplican proyectos corporativos de BI toolarge escala así. Mediante Data Catalog, su organización puede mejorar cualquier esfuerzo que implique un proceso manual de detección de orígenes de datos.

## <a name="scenario-3-capturing-tribal-knowledge"></a>Escenario 3: captura de conocimientos tribales
¿Cómo puede saber qué datos necesita toodo su trabajo y dónde toofind esos datos?

Si ha estado en su trabajo durante un tiempo, probablemente lo sepa. Terminar un proceso de aprendizaje de gradual y con el tiempo que ha aprendido sobre orígenes de datos de Hola que son trabajo cotidiano tooyour clave.

Cuando el equipo une a un nuevo empleado, ¿cómo esa persona saber qué datos están necesarios para el trabajo de hello y dónde toofind él?

Lo más probable es, nueva persona de hello procede tooyou con estas preguntas.

Esta transferencia en curso del conocimiento tribal forma parte del proceso de detección de origen de datos de hello en organizaciones grandes y pequeñas. Miembros del equipo más altos y experimentados han generado conocimientos durante años de hello, y los miembros del equipo más reciente han aprendido tooask cuando tienen preguntas. Hola más la información esencial a menudo sólo existe en cabezales de Hola de algunas personas claves, y cuando las personas están en vacaciones o dejaran el equipo de hello, organización Hola sufre.

Expertos en datos normalmente realizar un esfuerzo toodocument sus conocimientos, compartirlo por correo electrónico o de documentos de Word en un sitio de SharePoint del equipo. Aunque este planteamiento puede ser útil, presenta un problema de detección nuevo: ¿cómo personas saber qué documentación existe y dónde toofind él?

Con Azure Data Catalog, su organización tiene una única ubicación central para almacenar y compartir estos conocimientos tribales y para facilitar su detección. En el catálogo de datos, los expertos en datos pueden anotar los activos de datos directamente y se proporcionan vínculos tooexisting documentación. Cuando los miembros de la organización usa Hola catálogo toodiscover un origen de datos, encontrarán no solo el origen de hello propio, sino también conocimiento Hola que existía anteriormente sólo en las mentes de Hola de expertos en su organización.
