---
title: "información general detallada de planes de aaaAzure servicio de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo funcionan los planes del Servicio de aplicaciones de Azure y cómo benefician a su experiencia de administración."
keywords: servicio de aplicaciones, servicio de aplicaciones de azure, escala, escalable, plan del servicio de aplicaciones, costo del servicio de aplicaciones
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Introducción detallada sobre los planes del Servicio de aplicaciones de Azure

Planes de servicio de aplicaciones representan colección Hola de recursos físicos que usa toohost sus aplicaciones.

Los planes de App Service definen lo siguiente:

- Región (oeste de EE. UU., este de EE. UU., etc.)
- Recuento de escala (uno, dos, tres instancias, etc.)
- Tamaño de la instancia (pequeño, mediano, grande)
- SKU (Gratis, Compartido, Básico, Estándar y Premium)

Web Apps, Mobile Apps, Function Apps (o Funciones) o API Apps, en [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) se ejecutan todas en un plan de App Service.  Aplicaciones de hello misma suscripción y región pueden compartir un plan de servicio de aplicaciones. 

Todas las aplicaciones asignan tooan **plan de servicio de aplicaciones** compartir recursos de hello definidos por dicha. Compartir ahorra dinero al hospedar varias aplicaciones en un único plan de App Service.

Su **plan de servicio de aplicaciones** puede escalarse desde **libre** y **Shared** SKU demasiado**básica**, **estándar**, y **Premium** SKU que lo que le proporciona acceso a recursos de toomore y características a lo largo de hello forma.

Si su plan de servicio de aplicaciones se establece demasiado**básica** SKU o superior, a continuación, puede controlar hello **tamaño** y escalar el recuento de hello las máquinas virtuales.

Por ejemplo, si el plan está configurado toouse dos instancias de "pequeño" en el nivel de servicio estándar de hello, todas las aplicaciones que están asociadas a ese plan se ejecutan en ambas instancias. Aplicaciones también tienen características de nivel de servicio estándar de acceso toohello. Las instancias del plan en las que se ejecutan las aplicaciones están totalmente administradas y tienen una alta disponibilidad.

> [!IMPORTANT]
> Hola **SKU** y **escala** de servicio de aplicaciones de hello plan determina Hola costo y no Hola el número de aplicaciones hospedadas en ella.

Este artículo explora características clave de hello, como capa de escala de un plan de servicio de aplicaciones y cómo entran en juego al administrar sus aplicaciones.

## <a name="apps-and-app-service-plans"></a>Aplicaciones y planes del Servicio de aplicaciones

Una aplicación del Servicio de aplicaciones se puede asociar a un solo plan de dicho servicio en un momento determinado.

Tanto las aplicaciones como los planes se incluyen en un **grupo de recursos**. Un grupo de recursos actúa como límite de ciclo de vida de Hola para todos los recursos que está dentro de él. Puede usar recursos grupos toomanage todas las piezas de Hola de una aplicación juntos.

Dado que un grupo de recursos solo puede tener varios planes de servicio de aplicaciones, puede asignar diferentes aplicaciones toodifferent los recursos físicos.

Por ejemplo, puede separar los recursos entre entornos de desarrollo, pruebas y producción. Tener entornos independientes para producción y desarrollo o pruebas le permite aislar los recursos. De esta manera, pruebas de carga con una nueva versión de las aplicaciones no compiten por hello mismo recursos como las aplicaciones de producción, que prestan servicio a los clientes reales.

Al tener varios planes en un único grupo de recursos, también puede definir una aplicación que se extienda entre regiones geográficas.

Por ejemplo, una aplicación de alta disponibilidad que se ejecute en dos regiones incluirá dos planes como mínimo, uno por cada región, y una aplicación asociada a cada plan. En esta situación, todas las copias de Hola de aplicación hello, a continuación, se incluyen en un único grupo de recursos. Tener un grupo de recursos con varios planes y varias aplicaciones hace fácil toomanage, control y ver el estado de aplicación Hola Hola.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Creación de un plan de App Service o uso de uno ya existente

Al crear una aplicación, debe considerar la creación de un grupo de recursos. En Hola otra parte, si esta aplicación es un componente de una aplicación mayor, créelo en grupo de recursos de Hola que se asigna para esa aplicación mayor.

Si la aplicación hello es una aplicación completamente nueva o parte de otro más grande, puede elegir toouse un toohost plan existente, o crear uno nuevo. Esta decisión es más bien una cuestión de capacidad y de carga esperada.

Se recomienda aislar la aplicación en un nuevo plan de App Service en los siguientes casos:

- La aplicación consume muchos recursos.
- Aplicación tiene diferentes factores de escala de hello otras aplicaciones hospedadas en un plan existente.
- La aplicación necesita recursos de una región geográfica diferente.

De esta forma, puede asignar un nuevo conjunto de recursos para la aplicación y tener un mayor control de las aplicaciones.

## <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

> [!TIP]
> Si tiene un entorno de servicio de aplicaciones, puede revisar Hola documentación específica tooApp entornos del servicio aquí: [crear un plan de servicio de aplicaciones en un entorno de servicio de aplicaciones](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Puede crear un plan de servicio de aplicaciones vacío de hello experiencia de exploración del plan de servicio de aplicaciones o como parte de la creación de la aplicación.

Hola [portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil**y, a continuación, seleccione **aplicación Web** o en otro tipo de aplicación de servicio de aplicaciones.

![Crear una aplicación Hola portal de Azure.][createWebApp]

A continuación, puede seleccionar o crear plan de servicio de aplicaciones para la nueva aplicación de Hola Hola.

 ![Creación de un plan del Servicio de aplicaciones.][createASP]

toocreate un plan de servicio de aplicaciones, haga clic en **[+] crear nuevos**, Hola de tipo **plan de servicio de aplicaciones** nombre y, a continuación, seleccione un **ubicación**. Haga clic en **tarifa**y, a continuación, seleccione un nivel de precios adecuado para el servicio de Hola. Seleccione **todas las ver** tooview más precios opciones, como **libre** y **Shared**. Después de haber seleccionado el nivel de precios de hello, haga clic en hello **seleccione** botón.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Mover un plan de servicio de aplicaciones diferentes de aplicaciones tooa

Puede mover un plan de servicio de aplicaciones diferentes de aplicaciones tooa Hola [portal de Azure](https://portal.azure.com). Puede mover aplicaciones entre planes siempre sea planes Hola Hola mismo grupo de recursos y la región geográfica.

toomove un plan de tooanother de aplicación:

- Navegue aplicación toohello que desea toomove.
- Hola **menú**, busque hello **Plan de servicio de aplicaciones** sección.
- Seleccione **plan de servicio de aplicaciones de cambio** toostart proceso de Hola.

**Plan de servicio de aplicaciones de cambio** abre hello **plan de servicio de aplicaciones** selector. En este momento, puede seleccionar esta aplicación en un toomove de plan existente.

> [!IMPORTANT]
> plan de servicio de aplicaciones seleccione Hola interfaz de usuario se filtra por hello siguiendo criterios:
> - Existe dentro de hello mismo grupo de recursos
> - Existe en hello misma región geográfica
> - Existe dentro de hello mismo espacio Web
>
> Un espacio web es una construcción lógica dentro de App Service que define una agrupación de recursos del servidor. Una región geográfica (por ejemplo, oeste de Estados Unidos) contiene muchos espacios Web en orden tooallocate a los clientes usar servicio de aplicaciones. Actualmente, los recursos del servicio de aplicación no están toobe pueden movido entre espacios Web.
>

![Selector de plan del Servicio de aplicaciones.][change]

Cada plan tiene su propio plan de tarifa. Por ejemplo, mover un sitio desde un nivel de estándar de tooa nivel gratis, habilita todas las aplicaciones asignadas características de tooit toouse hello y recursos de nivel estándar de Hola.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Clonar un plan de servicio de aplicaciones diferentes de aplicaciones tooa

Si desea que la región diferente de toomove Hola aplicación tooa, una alternativa es la aplicación de clonación. La clonación hará una copia de su aplicación en un plan de App Service nuevo o existente en cualquier región.

Puede encontrar **clonar aplicación** en hello **herramientas de desarrollo** sección del menú de Hola.

> [!IMPORTANT]
> La clonación presenta algunas limitaciones sobre las que puede leer en [Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Escalación de un plan del Servicio de aplicaciones

Hay tres tooscale formas un plan:

- **El nivel de precios del plan de cambio hello**. Un plan en el nivel básico de hello puede ser tooStandard convertido y todas las aplicaciones asignan tooit toouse características Hola de nivel estándar Hola.
- **Cambiar el tamaño de las instancias del plan de hello**. Por ejemplo, un plan en el nivel básico de Hola que usa instancias pequeñas puede ser instancias grandes de toouse modificadas. Todas las aplicaciones que están asociadas a ese plan ahora pueden usar memoria adicional de Hola y recursos de CPU que Hola ofertas de tamaño mayor de instancia.
- **Cambiar el número de instancias del plan de hello**. Por ejemplo, un plan estándar que se escala toothree instancias puede ser instancias de escalado too10. Un plan de Premium se puede escalar horizontalmente too20 instancias (asunto tooavailability). Todas las aplicaciones que están asociadas a ese plan ahora pueden usar memoria adicional de Hola y recursos de CPU que Hola mayores ofertas de recuento de instancia.

Puede cambiar Hola tamaño de instancia y de nivel de precios haciendo clic en hello **escalar vertical** elemento bajo Configuración de aplicación hello ni Hola plan de servicio de aplicaciones. Cambios aplican toohello plan de servicio de aplicaciones y afecta a todas las aplicaciones que lo hospeda.

 ![Tooscale de valores de conjunto de seguridad de una aplicación.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Limpieza del plan de App Service

> [!IMPORTANT]
> **Planes de servicio de aplicaciones** que no tienen ningún toothem aplicaciones asociadas seguirán generando cargos puesto que continúan capacidad de cálculo de tooreserve Hola.

tooavoid inesperados cargos, cuando se elimina la aplicación última hello hospedada en un plan de servicio de aplicaciones, Hola vacío resultante también se elimina el plan de servicio de aplicaciones.

## <a name="summary"></a>Resumen

Los planes del Servicio de aplicaciones representan un conjunto de características y capacidades que puede compartir entre las aplicaciones. Los planes de servicio de aplicaciones permiten Hola conjunto de tooa de flexibilidad tooallocate aplicaciones específicas de recursos y optimizar aún más la utilización de recursos de Azure. De este modo, si desea que toosave dinero en su entorno de pruebas, puede compartir un plan entre varias aplicaciones. Asimismo, puede escalarlo entre varias regiones y planes para maximizar el rendimiento del entorno de producción.

## <a name="whats-changed"></a>Lo que ha cambiado

- Para que un cambio de toohello Guía de tooApp servicio de sitios Web, vea: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
