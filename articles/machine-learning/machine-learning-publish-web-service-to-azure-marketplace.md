---
title: "máquina de publicación de aaa(deprecated) tooAzure de servicio web Marketplace de aprendizaje | Documentos de Microsoft"
description: "(desusado) Cómo toopublish su toohello de servicio de Web de aprendizaje de máquina de Azure Marketplace de Azure"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(desusado) Publicar el servicio Web de Azure Machine Learning toohello Azure Marketplace

> [!NOTE]
> DataMarket y Data Services están en proceso de retirada, y las suscripciones existentes se retirarán y cancelarán a partir del 31 de marzo de 2017. Como resultado, este artículo se ha quedado obsoleto. 
> 
> Como alternativa, puede publicar su toohello de experimentos de aprendizaje automático [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/) para beneficio de Hola de comunidad de ciencia de datos de Hola. Para obtener más información, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hola Azure Marketplace permite Hola servicios web de aprendizaje automático de Azure de toopublish como pagados o liberar servicios para su uso por clientes externos. Este artículo proporciona información general de dicho proceso con vínculos tooguidelines tooget que se inició. Mediante el uso de este proceso, puede hacer que los servicios web disponibles para otro tooconsume a los desarrolladores en sus aplicaciones.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Información general del proceso de publicación de Hola
siguiente Hola es pasos de Hola para publicar un tooAzure de servicio web de aprendizaje automático de Azure Marketplace:

1. Crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático
2. Implementar Hola servicio tooproduction y obtener información de extremo de OData y clave de API de Hola.
3. Dirección URL de Hola de uso de hello publicado toopublish de servicio web demasiado[Azure Marketplace (mercado de datos)](https://publish.windowsazure.com/workspace/) 
4. Una vez que se envía, se revisa su oferta y necesita toobe aprobada antes de sus clientes podrán compras. proceso de publicación de Hello puede tardar unos días laborables. 

## <a name="walk-through"></a>Tutorial
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Paso 1: crear y publicar un servicio de solicitud-respuesta (RRS) de Aprendizaje automático
 Si no lo ha hecho todavía, consulte este [tutorial](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Paso 2: Implementar Hola servicio tooproduction y obtener información de extremo de OData y clave de API de Hola
1. De hello [Portal clásico de Azure](http://manage.windowsazure.com), seleccione hello **aprendizaje automático** opción de barra de navegación izquierda de Hola y seleccione el área de trabajo. 
2. Haga clic en hello **servicios WEB** ficha y seleccione hello web servicio le gustaría toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Seleccionar extremo de hello como toohave Hola marketplace consumiría. Si no ha creado ningún punto de conexión adicional, puede seleccionar hello **predeterminado** punto de conexión.
4. Una vez que haya hecho clic en el extremo de hello, será capaz de toosee hello **clave de API**. Necesitará esta información más adelante en el paso 3, por lo que se aconseja que la copie.
   
    ![Azure Marketplace][apikey]
5. Haga clic en hello **solicitud/respuesta** toohello marketplace de servicios de método, en este momento no se admite publicar la ejecución por lotes. Esto le llevará página de Ayuda de toohello API de hello método de solicitud/respuesta.
6. Hola copia **dirección de extremo de OData**, necesitará esta información más adelante en el paso 3.
   
    ![Azure Marketplace][odata]

implementar el servicio de hello en producción.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Paso 3: Dirección URL de Hola de uso de hello publica web servicio toopublish tooAzure Marketplace (DataMarket)
1. Navegue demasiado[Azure Marketplace (mercado de datos)](http://datamarket.azure.com/home) 
2. Haga clic en hello **publicar** vínculo situado en la parte superior de Hola de página de Hola. Esto le llevará toohello [Portal de publicación de Microsoft Azure](https://publish.windowsazure.com)
3. Haga clic en hello **publicadores** sección tooregister como un publicador.
4. Cuando cree una nueva oferta, elija **Servicios de datos** y, a continuación, haga clic en **Crear un nuevo servicio de datos**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. En **Planes** , deberá proporcionar información sobre su oferta, junto con un plan de precios. Decida si ofrecerá un servicio gratuito o de pago. tooget de pago, proporcionan información de pago como su información bancaria y de impuestos.
6. En **Marketing** proporcionan información acerca de su oferta, como el título de hello y una descripción para su oferta.
7. En **precios** puede establecer el precio de Hola para los planes para países específicos, o deje que el sistema de Hola "autoprice" su oferta.
8. En hello **servicio de datos** , haga clic en **servicio Web** como hello **origen de datos**.
   
    ![Azure Marketplace][image2]
9. Obtener hello web service URL y API de la clave de hello Portal clásico de Azure, tal como se describe en el paso 2 anterior.
10. En el cuadro de diálogo de configuración de servicio de datos de Marketplace de hello pegue dirección del extremo de OData de hello en hello **dirección URL del servicio** cuadro de texto.
11. Para **autenticación**, elija **encabezado** como hello **esquema de autenticación**.
    
    * Escriba "Autorización" de hello **nombre de encabezado**.
    * Para hello **valor del encabezado**, escriba "Portador" (sin las comillas de hello), haga clic en hello **espacio** barra y, a continuación, pegue la clave de API de Hola.
    * Seleccione hello **este servicio es OData** casilla de verificación.
    * Haga clic en **Probar conexión** conexión de hello tootest.
12. En **Categorías**, asegúrese de que **Machine Learning** esté seleccionado.
13. Cuando haya terminado de especificar todos Hola metadatos acerca de su oferta, haga clic en **publicar**y, a continuación, **Push tooStaging**. En este momento, se le notificará de los problemas restantes que necesita toofix.
14. Una vez se haya asegurado de finalización de todas las cuestiones pendientes de hello, haga clic en **solicitar aprobación toopush tooProduction**. proceso de publicación de Hello puede tardar unos días laborables. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

