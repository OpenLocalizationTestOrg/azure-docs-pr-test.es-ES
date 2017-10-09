---
title: "aaaTest oferta de la máquina virtual para hello Marketplace | Documentos de Microsoft"
description: "Comprender cómo tootest imagen de la máquina virtual para hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Probar su oferta VM para hello Azure Marketplace en almacenamiento provisional
Significa que implementar el SKU en privado "espacio aislado" donde pueda probar y validar su funcionalidad antes de implementarla toohello Marketplace de almacenamiento provisional. Hola SKU aparece en ensayo tal como lo haría a tooa cliente que ha implementado. La imagen de máquina virtual debe ser toostaging toobe certificadas insertado.

## <a name="step-1-push-your-offer-toostaging"></a>Paso 1: Insertar su toostaging de oferta
1. En hello **publicar** , haga clic en **Push tooStaging**.
   
    ![dibujo](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Si el Portal de publicación de hello le informa de los errores, corríjalos.
3. Hola **quién puede acceder a su oferta preconfigurada?** diálogo cuadro, escriba Hola lista de suscripciones de Azure que va a usar toopreview su oferta en hello [portal de vista previa](https://portal.azure.com).
   
   > [!NOTE]
   > En el caso de las plantillas de soluciones y máquinas virtuales, **no** agregue a la lista blanca suscripciones de tipo CSP, DreamSpark o Azure bajo licencia Open.
   > 
   > 

    > En el caso de máquinas virtuales, al hacer clic en el botón de hello **tooSTAGING de INSERCIÓN**, Hola siguiendo los pasos que se llevan a cabo detrás de escena Hola. Será capaz de tooview progreso de Hola de cada paso en la ficha de la publicación de Hola Hola portal de publicación. Debe comprobar esta página en intervalos regulares (hasta que el estado de hello muestra almacenado PROVISIONALMENTE) para cualquier información de error que necesita corrección desde el final.

    > - En primer lugar la solicitud de almacenamiento provisional va toohello equipo de certificación que validar Hola vhd. Sin embargo, si la solicitud tiene solo cambio de marketing, Hola certificación paso se omitirá.
    > - Una vez completada la certificación de hello, replicación de inicio de la oferta de hello en todas las Hola centros de datos de Azure. Por lo general toma 24-48hours para toocomplete de replicación de Hola pero puede tardar una semana tooa según tamaño Hola de hello disco duro virtual. Sin embargo, si la solicitud tiene solo cambio de marketing, replicación de hello es más rápida.
    > - Una vez completada la replicación hello, a continuación, oferta Hola estarán disponible en hello [portal de Azure](http:/portal.azure.com). En ese Hola de tiempo se convierten en ensayo estado Hola portal de publicación. Una oferta de ensayada está visible en hello [portal de Azure](http:/portal.azure.com) únicamente con los identificadores de correo electrónico de hello asociados con qué hello intermedia oferta de suscripción de Hola.

1. Inicie sesión en toohello [portal de vista previa](https://portal.azure.com) mediante uno de hello las suscripciones de Azure aparecen en el paso anterior de Hola.
2. Busque su oferta y valide los puntos de su imagen de VM:
   
   * Asegúrese de que contenido de marketing aparece correctamente en hello Marketplace.
   * Implementación to-end de la imagen de máquina virtual de Hola.
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Su oferta permanecerá en almacenamiento provisional hasta que notificar a Microsoft a través del Portal de publicación de hello [**publicar** ficha > haga clic en el botón de hello **"Solicitar aprobación tooPush tooProduction"**] que está listo toopush tooproduction. Se trata de un toohave tiempo ideal que comprobación todos los miembros del equipo a través de todo el contenido de preparación para la oferta va enumeradas.
> 
> Hola plataforma de almacenamiento provisional está diseñada para pruebas oferta de hello en un modo de vista previa por publicador Hola. Se desaconseja encarecidamente usar esta plataforma con fines comerciales.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ahora que su oferta "intermedia" y haya probado la funcionalidad y el contenido de marketing, puede continuar la publicación final toohello fase, **paso 4**: [implementar el Marketplace de oferta toohello](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Otras referencias
* [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)

