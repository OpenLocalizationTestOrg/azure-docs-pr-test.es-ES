---
title: aaaDeploy su toohello oferta Azure Marketplace | Documentos de Microsoft
description: "Obtenga información acerca de y recorra Hola instrucciones toodeploy su oferta: imagen de máquina virtual, el servicio de programador, servicio de datos, etc.--toohello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Implementar la toohello oferta Azure Marketplace
Cuando esté satisfecho con la oferta (es decir, que haya probado los escenarios de clientes, marketing de contenido, etc.) y está listo toolaunch, solicitud **Push tooproduction** en hello **publicar** ficha.  

1. Hola cuatro pasos en la página del tutorial Hola Hola portal de publicación debe ser completado y verde. Para las ofertas de la máquina Virtual, asegúrese de que se siguen ese Hola siguiendo las instrucciones.
   
    ![dibujo][img-pubportal-walkthru-checked]
2. Seleccione hello **publicar** pestaña en la lista de Hola Hola lado izquierdo.
   
    ![dibujo][img-pubportal-menu-publish]
3. Haga clic en el botón de hello **solicitar aprobación toopush tooproduction**. Una vez que se realiza la solicitud de Hola, equipo de aprobación de hello ejecuta una revisión final y, a continuación, su oferta, estará disponible en hello Azure Marketplace.
   
    ![dibujo][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> En el caso de máquinas virtuales, al hacer clic en hello tooproduction de toopush de aprobación de solicitud de botón, Hola pasos se realiza detrás de escena Hola. Será capaz de tooview progreso de Hola de cada paso en la ficha de la publicación de Hola Hola portal de publicación. Debe comprobar esta página en intervalos regulares (hasta que el estado de hello muestra "Listada") para cualquier información de error que necesita corrección desde el final.
> 
> * En primer lugar la solicitud de producción va toohello equipo de certificación que validar Hola vhd. Sin embargo, si está actualizando su oferta ya enumerado y solicitud de hello tiene solo cambio de marketing, Hola certificación paso se omitirá.
> * En el paso siguiente de hello, solicitud de hello proceder toohello equipo de validación del contenido que compruebe Hola contenido de la oferta de Hola de marketing.
> * Si Hola por encima de los pasos se realizan correctamente, se aprueba oferta hello en producción. En este momento, el estado de Hola se convierten en "muestra" en el portal de publicación de Hola. Sin embargo, este estado de "Listada" no implica que el proceso de hello está completado. Hola siguiendo los pasos necesidad toobe finalice antes de la oferta de hello está disponible en hello Azure Marketplace.
> * Una vez aprobada la oferta de hello en producción en el paso de hello anterior, la replicación de inicio de la oferta de hello en todas las Hola centros de datos de Azure. Por lo general toma 24-48hours para toocomplete de replicación de Hola pero puede tardar una semana tooa según tamaño Hola de hello disco duro virtual. Sin embargo, si está actualizando su oferta ya enumerado y tiene una capacidad solo cambio de marketing, replicación de hello es más rápida.
> * Una vez completada la replicación hello, oferta Hola estará disponible en hello Azure Marketplace.
> 
> Oferta de hello siempre se puede eliminar mientras se encuentra en un **borrador** estado (es decir, nunca **Push toostaging** o **Push tooproduction**). En hello **historial** , haga clic en hello **Descartar borrador** situado en la parte inferior de Hola de hello página toodelete un borrador.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Lista de comprobación de producción para todas las ofertas de máquinas virtuales
* Asegúrese de ser asociado Microsoft Azure Certified.
* En la ficha de SKU de hello, opción de Hola "ocultar esta SKU de hello Marketplace porque siempre debe ser comprado a través de una plantilla de solución" se debe marcar como sí solo si Hola SKU es una parte de una plantilla de solución. En todos los Hola otros casos, esta opción siempre debe estar marcada como NO.
* Recuerde: No debería cambiar configuración de visibilidad SKU de hello una vez que se muestra hello SKU. No se admite esta funcionalidad.
* Asegúrese de que los logotipos de Hola cumplan las directrices de logotipo de Azure Marketplace toohello indicadas a continuación.
* La descripción de la oferta y la SKU no debe ser la misma.
* El título de la SKU y el resumen largo de la oferta no deben ser los mismos.
* El título de la SKU y el resumen de la oferta no deben ser los mismos.
* Los títulos de la SKU no deben ser idénticos para una oferta con varias SKU.

**Instrucciones del logotipo de Azure Marketplace**

* Hola diseño de Azure tiene una paleta de colores simple. Mantener número Hola de principal y los colores de la base de datos secundaria en el logotipo baja.
* colores del tema Hola de hello portal de Azure son blancos y negros. Por lo tanto, evite usar estos colores como color de fondo de Hola de los logotipos. Usar algunos colores que podría hacer que sus logotipos destacan en hello portal de Azure. Nosotros recomendamos usar colores primarios simples. Si utilizas un fondo transparente, asegúrese de que ese logotipo/texto hello no es blanco o negro.
* No utilice un fondo degradado en logotipo Hola.
* Evite colocar texto, incluso la empresa o el nombre de marca, en el logotipo de Hola.
* Hola apariencia y funcionamiento de su logotipo debe ser "plano" y debe evitar degradados.
* logotipo de Hello no debe ajustarse.

**Instrucciones adicionales para el logotipo de héroe de hello:**

* logotipo de héroe de Hello es opcional. publicador de Hello puede elegir no tooupload un logotipo héroe. **Sin embargo cuando se han cargado Hola héroe icono no se puede eliminar de hello portal de publicación. En ese momento, socio Hola debe seguir instrucciones de Azure Marketplace de Hola por iconos héroe else oferta hello no será posible tooproduction aprobada.**
* Mostrar nombre del publicador, Hola y el título de la SKU de Hello ofrecen resumen largo se muestran en color de fuente blanca. Por lo tanto, debe evitar mantener cualquier color claro en fondo Hola Hola héroe icono. Los fondos transparentes y de color negro y blanco no pueden utilizarse en las imágenes prominentes.
* Hello DisplayName del publicador, título SKU, resumidas largas de oferta de Hola y Hola botón crean se incrustan mediante programación dentro de logotipo héroe de hello una vez que la oferta de hello queda enumerada. Por lo que no debe escribir cualquier texto mientras se diseñan logotipo héroe de Hola. Deje espacio vacío en derecha Hola puesto texto de hello (es decir, nombre de presentación del publicador, título SKU, oferta Hola resumida largas) se incluirán mediante programación con nosotros a través de allí. espacio vacío de Hola para texto hello debe ser 415 x 100 en hello derecho (y se desplaza por 370px de hello izquierda).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Lista de comprobación de producción adicional para ofertas de máquinas virtuales ya activas
* Compruebe que si ya hay una oferta con hello mismo ofrecen el nombre de su empresa. Si es así, debe agregar una nueva versión de hello SKU de la oferta existente de hello en lugar de crear una nueva oferta duplicada.
* Disco de datos no debe cambiar entre las dos versiones de hello misma SKU.
* Hello Azure Marketplace no es compatible con precios de cambio de hello aparecen SKU puesto que afecta a la facturación de los clientes existentes de Hola Hola. Asegúrese de que no cambian Hola precios de SKU de hello enumerado en regiones de Hola donde hello SKU no está disponible. Sin embargo, puede agregar SKU nueva o agregar nuevas tooan regiones existentes SKU.

## <a name="next-steps"></a>Pasos siguientes
Una vez oferta Hola esté activa, probar toovalidate de escenarios de cliente hello que todos los contratos de Hola y funcionalidad funcionan correctamente en el entorno de producción de hello como entorno de ensayo de hello probados y validados.

## <a name="see-also"></a>Otras referencias
* [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
