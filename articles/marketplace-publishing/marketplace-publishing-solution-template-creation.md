---
title: "aaaGuide toocreating una plantilla de solución para hello Marketplace | Documentos de Microsoft"
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar una plantilla de solución de imagen de varias VM a la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Guía de toocreate una plantilla de solución de Azure Marketplace
Después de completar el paso 1, [creación de cuentas y registro][link-acct-creation], se le han guiado durante la creación de hello de una plantilla de solución de Azure compatible en [técnicos requisitos previos para crear un plantilla de solución](marketplace-publishing-solution-template-creation-prerequisites.md). Ahora se le guiará por los pasos de Hola para crear una plantilla de solución para varias máquinas virtuales en hello [Portal de publicación] [ link-pubportal] para hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Crear su oferta de la plantilla de solución en hello Portal de publicación
Vaya demasiado [https://publish.windowsazure.com](http://publish.windowsazure.com). Al iniciar sesión por hello primera hora toohello [Portal de publicación](https://publish.windowsazure.com/), Hola uso misma cuenta con la que se registró el perfil de vendedor de su empresa. Más adelante, puede agregar a cualquier empleado de la empresa como Coadministrador en hello Portal de publicación.

### <a name="1-select-solution-templates"></a>1. Selección de "Plantillas de solución"
  ![dibujo][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Creación de una plantilla de solución
  ![dibujo][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Comienzo con topologías
Una plantilla de solución es un tooall "primario" de sus topologías. Puede definir varias topologías en una oferta o plantilla de solución. Cuando una oferta se inserta toostaging, se inserta con todos sus topologías. Siga estos pasos hello toodefine su oferta:     

* Crear una topología: "Identificador de topología" suele ser nombre Hola de topología de hello para la plantilla de solución de Hola. identificador de topología de Hola se usa en la dirección URL de hello tal y como se muestra a continuación:

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}

  Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}
* Adición de una nueva versión

### <a name="4-get-your-topology-versions-certified"></a>4. Certificación de las versiones de topología
Cargar un archivo zip que contiene una versión concreta del topología Hola de tooprovision de todos los archivos necesarios. Este archivo zip debe contener la siguiente hello:

* Los archivos *mainTemplate.json* y *createUiDefinition.json* en su directorio raíz.
* Las plantillas vinculadas y todos los scripts requeridos.

  > [!TIP]
  > Mientras los desarrolladores trabajan sobre cómo crear soluciones de hello topologías de plantilla y obtenerlas certificada, negocio hello, departamentos de marketing o legales de la empresa pueden trabajar en el contenido de marketing y legal de Hola.
  >
  >

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado la plantilla de solución y cargado el archivo zip de hello, siga las instrucciones de Hola Hola [Guía de contenido de marketing de Marketplace](marketplace-publishing-push-to-staging.md) antes de insertar Hola oferta toostaging. conjunto completo de hello toosee de marketplace publicar artículos, visite [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md).

Es posible que también le interesen los siguientes artículos relacionados:

* Imágenes de máquinas virtuales: [Acerca de las imágenes de máquina virtual en Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Extensiones de VM: [Información general del agente de máquina virtual y las extensiones de VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) y [Características y extensiones de máquina virtual de Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) y [Ejemplos sencillos de plantillas](https://github.com/rjmax/ArmExamples)
* Limita la cuenta de almacenamiento: [cómo tooMonitor para la limitación de la cuenta de almacenamiento](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) y [almacenamiento Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
