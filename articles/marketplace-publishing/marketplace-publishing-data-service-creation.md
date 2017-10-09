---
title: aaaGuide toocreating un servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar un servicio de datos para la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Guía de publicación de servicio de datos para hello Azure Marketplace
> [!IMPORTANT]
> **En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.** Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners). Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Después de completar el paso 1, de hello [creación de cuentas y el registro](marketplace-publishing-accounts-creation-registration.md), se le guiará a través de hello [General técnica](marketplace-publishing-pre-requisites.md) y [requisitos técnicos](marketplace-publishing-data-service-creation-prerequisites.md) de un servicio de datos se ofrecen en Azure Marketplace. Ahora se le guiará por los pasos de Hola para crear una oferta de servicio de datos en hello [Portal de publicación] [ link-pubportal] para hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Inicio de sesión toohello Portal de publicación.
Vaya demasiado[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Para la primera hora inicio de sesión tooPublishing Portal, usar hello misma cuenta con la que generar perfiles de vendedor de su empresa se ha registrado en el Centro para desarrolladores.**  (Más adelante puede agregar a cualquier empleado de la empresa como Coadministrador en hello Portal de publicación).

Haga clic en hello **publicar los servicios de datos** icono si éste es el primer inicio de sesión hello en el portal de publicación de Hola.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Elija **Data Services** en el menú de navegación Hola Hola lado izquierdo.
  ![dibujo](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Creación de un nuevo servicio de datos
Rellene el título de hello para la oferta de servicio de datos nueva y haga clic en "+" en hello derecho.

  ![dibujo](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Submenú Hola revisión en hello recién creado del servicio de datos de menú de navegación de Hola.
Haga clic en hello **tutorial** pestaña y revise todos los pasos necesarios necesarios toopublish correctamente Hola servicio de datos en hello Azure Marketplace.

> [!TIP]
> Siempre puede haga clic en vínculos de hello en la página del "Tutorial" Hola o utilizar las pestañas en el submenú de la oferta de servicio de datos de hello en el lado izquierdo de Hola.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Creación de un nuevo plan
### <a name="offers-plans-transactions"></a>Ofertas, Planes, Transacciones
Cada Oferta puede tener varios Planes, pero debe tener al menos un (1) Plan. Cuando los usuarios finales suscriben tooyour oferta se suscriben para una Plan del oferta de hello. Cada plan define cómo se realizarán los usuarios finales pueden toouse capaz de su servicio.

Actualmente Azure Marketplace admite transacciones de suscripción mensual según modelo solo para los servicios de datos, es decir, los usuarios finales pagará cargos mensuales según el precio de toohello de plan concreto de Hola que suscritos tooand será capaz de tooconsume cada número de mes de transacción definida por el plan de Hola.

Cada transacción normalmente definido como el número de registros que devolverá el servicio de datos basado en consulta de hello enviado toohello servicio. valor predeterminado de Hello es 100. Número de transacciones devuelto será tooeach consulta número de registros dividido entre 100 y redondea al entero más próximo toohello.

Es el servicio de Azure Marketplace capa responsabilidad toomonitor (metros) número de transacciones utilizados por cada consulta.

> [!IMPORTANT]
> Los usuarios finales que alcanza el límite de transacciones de Hola durante el mes de Hola se bloqueará impide continuar servicio de hello toouse hasta el final de su ciclo de suscripción mensual.
> 
> Hola plan o uno de los planes de hello puede (pero no debe) incluye un número ilimitado de transacciones.
> 
> 

### <a name="create-a-plan"></a>Cree un plan.
1. Haga clic en **"+"** toohello siguiente "Agregar un nuevo plan".
2. Elija una de las opciones de hello: **Unlimited** o **limitado** el uso de este plan.  Si limitado, a continuación, proporciona Hola número de transacciones Hola plan le permitirá tooconsume en un mes.
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Portal de publicación también sugerirá "Identificador de Plan de", que será usado toocommunicate toohello los usuarios finales Hola nombre del plan de Hola Hola interfaz de usuario de y también la usan hello tooidentify de servicio de mercado Hola Plan. Puede cambiar Hola "Identificador de Plan" Si desea.
   
   > [!NOTE]
   > Hola "Identificador de Plan" debe ser único dentro de ámbito de Hola de cada oferta. Como muchos otros identificadores usados en Hola Plan de Portal de publicación se bloqueará el identificador después de hello primer tooproduction de publicación y no estará toochange capaz de este identificador.
   > 
   > 
3. Haga clic en tooaccept su elección.
4. A continuación, se le harán algunas preguntas adicionales sobre el Plan recién creado.
   
    ![dibujo](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Pregunta | Significado |
| --- | --- |
| **¿Este Plan es gratuito y está disponible en todo el mundo?** |Puede crear un plan completamente gratuito. Si su Hola previsto sólo para esta oferta: significa que se va a publicar "Ofrecen libre" Hola Marketplace. Si es solo para una (de pocas) Plan, Hola le ofrece un toolearn de los usuarios finales de opción toooffer más información sobre el servicio con un número relativamente pequeño de transacciones al mes.  Si la respuesta de hello es "Sí", no se pedirá ningún preguntas más. |

> [!NOTE]
> Los usuarios finales siempre puede actualizar toohello planes de pago.
> 
> 

| Pregunta | Significado |
| --- | --- |
| **¿Hay una versión de evaluación gratuita disponible?** |Puede elegir entre "No prueba" en absoluto o proporcionar una opción toouse su Plan para "Un mes". Publicadores como toouse este beneficios opción tooprovide los usuarios finales Hola posibilidad toounderstand Hola de hello ofrecen de forma gratuita durante un mes. |

> [!IMPORTANT]
> Los usuarios finales solo será capaz de toopurchase una prueba gratuita si ha establecido el instrumento de pago por ejemplo, tarjeta de crédito, contrato enterprise.
> 
> Después de un mes de prueba gratuita de hello, Azure Marketplace iniciará cobrar a los clientes precio Hola hasta fecha de Hola de su suscripción de hello, a menos que el cliente de hello iniciada cancelación de suscripción de Hola. No se proporcionará ninguna notificación especial toohello los usuarios finales.
> 
> 

| Pregunta | Significado |
| --- | --- |
| **¿Este plan necesita un toopurchase de código de promoción?** |Publicadores tienen un tootheir de acceso de toolimit opción planes de servicio al proporcionar un código especial, denominado a "A Promocode" toospecific customers. Solo los usuarios finales que tendrán este Promocode será capaz de toosubscribe toohello Plan. Si elige "No", acepta que todos los usuarios de región de Hola donde ofrecen Hola están disponible (vea [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) para obtener más detalles) será capaz de toosubscribe toothis plan. No se le harán más preguntas. |
| **¿Ocultar también este plan a cualquier persona que no tenga un código de promoción válido?** |Si Hola respuesta toohello anterior pregunta es "Sí" hello publicador tiene una opción toocompletely suprimir este plan desde que aparecen en hello interfaz de usuario de hello Marketplace. Significa que, los clientes no podrán ver este plan en la página de detalles de la oferta de Hola. Los usuarios finales que recibirán un toopurchase promocode, serán tooit toosubscribe capaz de usar este promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Creación de contenido de marketing de Marketplace
Para cómo tooprovide información necesaria en **Marketing, precios, compatibilidad y categorías** pestañas, visitan [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) que es común artefactos tooall publicados en hello Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Conectar su tooyour de oferta de servicio (en función de SQL Azure o en función de servicio de Web).
Haga clic en hello **Data Services** submenú.

En la mitad superior de Hola de página Hola se le preguntará de oferta de hello tooprovide **Namespace**.  

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.png)

Hola por debajo de la pregunta definirá cómo Hola publicador va tooexpose recién creado oferta tooAzure Marketplace. (Para obtener más información, vea hello [Guía de requisitos previos Technical Data Services](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Publicar Hola servicio de basado en base de datos**

Haga clic en **Base de datos**. Hola después de la página se mostrará:

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate una asignación de CSDL para hello conjunto de datos se basa en hello base de datos de SQL Azure:

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.4.png)

Y, a continuación, para cada tabla

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.6.png)

Si Servicio web

  ![dibujo](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Lectura [asignación existente web tooOData de servicio a través de CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obtener instrucciones detalladas y ejemplos para crear un servicio Web de CSDL.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado su oferta de servicio de datos, asegúrese de completar las instrucciones de Hola Hola [Guía de contenido de Marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de continuar demasiado[probando el servicio de datos de almacenamiento provisional](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Otras referencias
* [Introducción: Cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)
* Si está interesado en conocer Hola proceso general de asignación de OData y su propósito, lea este artículo [asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definiciones, estructuras e instrucciones.
* Si está interesado en el aprendizaje y nodos de descripción Hola específicos y sus parámetros, lea este artículo [nodos de asignación de datos de servicio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para las definiciones y explicaciones, ejemplos y contexto de casos de uso.
* Si está interesado en Revisar ejemplos, lea este artículo [ejemplos de asignación de datos de servicios OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de ejemplo y comprender la sintaxis del código y el contexto.

[link-pubportal]:https://publish.windowsazure.com
