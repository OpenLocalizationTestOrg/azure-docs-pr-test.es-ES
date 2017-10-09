---
title: aaaTesting ofrecer el servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Comprender cómo tootest el servicio de datos ofrecen para hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Probar su oferta de Servicio de datos en Ensayo
> [!IMPORTANT]
> **En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.** Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners). Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Después de completar los dos primeros pasos de Hola de [crear su cuenta de Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) y [crear la oferta de servicio de datos en el Portal de publicación](marketplace-publishing-data-service-creation.md) está listo para hacer que su oferta disponible en hello Azure Marketplace. En este tema le guían a través de hello en primer lugar, intermedio, paso llamado "ensayo"

Significa que la implementación de la oferta en privado "espacio aislado" donde puede probar y comprobar su funcionalidad antes de insertar tooproduction de almacenamiento provisional. oferta de Hello aparecerá en ensayo tal como lo haría a tooa cliente que ha implementado.

## <a name="step-1-pushing-your-offer-toostaging"></a>Paso 1. Insertar su toostaging de oferta
Insertar su toostaging oferta permite oferta de hello tootest antes de que esté disponible toofuture suscriptores.  Puede ver cómo aparecerá su oferta y funcionar para aquellos que se suscriban tooyour datos.  

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Inicio de sesión en hello [Portal de publicación](https://publish.windowsazure.com)
2. Seleccione **Data Services** en la ventana de navegación izquierdo de hello
3. Seleccione la oferta que desee toopush toostaging. Verá Hola por encima de la pantalla.
4. Haga clic en **Push tooStaging** botón.  
5. Si hay problemas con hello oferta que sea necesario toobe había completado toostaging toopushing anterior, verá una lista que se muestra.  Corrija estos elementos, haga clic en cada elemento de lista de Hola. Cuando todas las correcciones realizadas, haga clic en **Push tooStaging** nuevamente en el botón.

Si no hay ningún problema con su oferta verá la ventana emergente de Hola a continuación.  

Si no estás planificación/no aprobado toosurface su oferta en el Portal de Azure (actualmente con una capacidad limitada), a continuación, ventana emergente de hello simplemente cierre.

tootest los datos del servicio en el Portal de Azure (en el portal de DataMarket de toohello de suma), necesitará un tootest de Id. de suscripción de Azure con.  Este identificador de suscripción identificará cuenta Hola que estará permitido tootest su oferta.  

Corte y pegue el identificador de la suscripción y haga clic en hello toocontinue de marca de verificación.

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Estos identificadores de las suscripciones de Azure solo son necesarias para las pruebas y almacenamiento provisional en hello [Portal de administración de Azure](https://manage.windowsazure.com). No son necesario tootest en Azure Marketplace.
> 
> 

Hello siguiente pantalla que aparece muestra que la publicación está teniendo lugar mostrando Hola "en curso" icono resaltado amarillo abajo. Insertar toostaging tarda entre 10 minutos de too15.  Si tarda más, primero actualice su explorador (presione F5 en Internet Explorer).  En casos excepcionales de Hola donde su oferta todavía está presionando toostaging después de una hora, haga clic en contacto Hola nos vincular toolet nos sabe que existe un problema.

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Cuando completa la tooStaging de inserción de Hola Hola "en curso" icono dejará de mover y se actualizará el estado de hello demasiado "ensayo".  Se está ahora listo tootest su oferta.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Paso 2: Probar su oferta almacenada provisionalmente en DataMarket
Haga clic en el vínculo de hello texto hello **"ver su servicio se ofrecen en..."** pantalla de bienvenida toodisplay que Hola suscriptor verá que su oferta pasa tooproduction y aparecerá en DataMarket.

  ![dibujo](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Probar o compruebe cada uno de hello 12 elementos marcados anteriormente tooensure todos los logotipos, precios/transacciones, texto, imágenes, documentación y vínculos son correctas y funcionen correctamente.  Se trata de un tooensure buen momento los valores de prueba que especificó al crear la oferta se han reemplazado por valores reales.

1. Logotipo de la oferta
2. Nombre de la oferta
3. Sitio Web de la compañía de publicador nombre/vínculo tooyour
4. Categorías de búsqueda para su oferta
5. Suscriptores de tooassist de vínculo de soporte técnico de su oferta
6. Descripción contextual de la oferta
7. Plan de oferta que describe los detalles de la facturación
8. Código de tooimplementation de vínculo
9. Imágenes de ejemplo que ilustran el uso de los datos de la oferta
10. Metadatos de entrada/salida para cada servicio en la oferta de Hola
11. Términos de uso de la oferta
12. Vista previa de los datos de la oferta de Hola

Finalmente, compruebe el servicio de hello trabajará en hello Datamarket haciendo clic en el vínculo de Hola "Explorar este conjunto de datos".  Se abrirá una nueva ventana de herramienta de hello llamamos "Explorador de servicios" para que pueda ver los resultados de Hola de una consulta en el servicio.  En esta ventana, puede especificar Hola parámetros necesitan y ver resultados de hello muestra de una consulta en el servicio.   Además, muestra es Hola URL para la consulta.  

> [!NOTE]
> Ser seguro descripción textual de Hola de tooreview del servicio de hello muestra en la parte superior de Hola.  Y si su oferta consta de más de un servicio llamar a, haga clic en las pestañas de hello en hello inferior tooswitch toohello siguiente servicio tooreview y prueban.
> 
> 

## <a name="next-step"></a>Paso siguiente
Si está teniendo problemas y necesita ayuda para resolverlos, póngase en contacto con el [soporte técnico para publicadores de Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Si está satisfecho y toopublish preparado su oferta, lea hello [tooProduction tooPush de aprobación de solicitud](marketplace-publishing-push-to-production.md) documentación.

## <a name="see-also"></a>Otras referencias
* [Introducción: Cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)

