---
title: "Preguntas más frecuentes: aaa(deprecated) publicar y usar aplicaciones de aprendizaje automático en Azure Marketplace | Documentos de Microsoft"
description: "(desusado) Preguntas más frecuentes sobre la publicación de aprendizaje automático de aplicaciones en hello Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(desusado) Publicación y uso de aplicaciones de aprendizaje automático en hello Azure Marketplace: preguntas más frecuentes

> [!NOTE]
> DataMarket y Data Services están en proceso de retirada, y las suscripciones existentes se retirarán y cancelarán a partir del 31 de marzo de 2017. Como resultado, este artículo se ha quedado obsoleto. 
> 
> Como alternativa, puede publicar su toohello de experimentos de aprendizaje automático [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/) para beneficio de Hola de comunidad de ciencia de datos de Hola. Para obtener más información, consulte [compartir y detectar los recursos Hola Galería de inteligencia de Cortana](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Preguntas acerca del consumo en Marketplace
**1. ¿Por qué recibo Hola siguiente mensaje de error después de que especifique la entrada para el servicio web de hello:**

**solicitud de Hello generó un error de back-end o back-end de tiempo de espera. equipo de Hello está investigando el problema de Hola. Sentimos las molestias de Hola. (500)**

Es podrán que los parámetros de entrada no cumpla toohello formato requerido para el servicio web específico de Hola. Consulte toohello correspondiente documentación vínculo toofind Hola formato correcto para parámetros de entrada y las limitaciones de Hola de este servicio web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Si Copiar vínculo Hola API de servicio de web de Hola que he visto en Hola "Explorar este conjunto de datos" página y pegarlo en otra ventana del explorador, ¿qué credenciales ¿utilizar tooaccess Hola resultado y ¿cómo veo ellos?**

Debe usar su cuenta de Marketplace como nombre de usuario de Hola y clave de cuenta principal de hello como contraseña de Hola. clave de cuenta principal de Hello puede encontrarse en hello **explorar este conjunto de datos** página en la descripción de hello del servicio web de hello (haga clic en hello **mostrar** botón). resultado de Hello puede mostrar en Explorador de Hola o puede estar disponible demasiado descarga, según el explorador que usa.

**3. ¿Por qué recibo Hola siguiente mensaje de error después de escribir entrada hello para el servicio web de hello en la página de "Explorar este conjunto de datos" hello:** 

**Se ha producido un error inesperado al procesar la solicitud. Vuelva a intentarlo.**

Uno o más parámetros de entrada del servicio web pueden ha superado el límite de longitud de hello al consumir servicio web de hello en marketplace hello **explorar este conjunto de datos** página. Servicios de Hola se pueden llamar con una longitud de entrada ya mediante métodos POST de HTTP. Para obtener ejemplos, vea [ejemplo soluciones que usan R en aprendizaje automático y publicado tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. ¿Por qué no aparece nada en Hola "Explorador de API" pestaña int Hola almacén Hola Portal clásico de Azure?** 

Se trata de un problema conocido con hello Azure Marketplace de Portal clásico. equipo de Hello funciona tooresolve este problema. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Preguntas acerca de la publicación desde Aprendizaje automático de Azure en Marketplace
**1. ¿Por qué mis transacciones de logotipos o imágenes no se actualizan en mi servicio web?** 

Logotipos e imágenes se almacenan en caché en el portal de publicación de Hola y pueden tardar hasta too10 días para el nuevo logotipo de Hola o tooupdate de imagen en el portal de Hola.

**2. ¿Por qué es la pestaña de "Detalles" hello de mi servicio web de Marketplace que muestra un mensaje de error?**

Hay un problema conocido de Marketplace al conectarse tooAzure aprendizaje automático para obtener detalles de servicio. equipo de Hello funciona tooresolve este problema.

**3. ¿Por qué no funciona Hola código de ejemplo de R en los servicios web de aprendizaje automático de Azure de Hola para consumir servicios web de hello en Marketplace?**

sistemas de autenticación de Hello son diferentes al conectarse directamente los servicios web de aprendizaje automático de tooAzure en comparación con los servicios web de tooconnecting toothese a través de hello Marketplace. Servicios de Hello en Marketplace son servicios de OData y se pueden llamar a los métodos GET o POST. 

**4. ¿Por qué los vínculos de soporte técnico de Hola de mi servicio web ofrece no actualizarse correctamente para algunos de Mis ofertas?**

vínculos de soporte técnico de Hello son globales por publicador, no para cada oferta. 

**5. ¿Cómo puedo publicar un servicio web con el modo de entrada por lotes en Marketplace?**

modo de entrada de lote de Hello, no se admite actualmente en servicios web de Marketplace.

**6. ¿Que debo ponerme en contacto con ayuda de tooget si tengo preguntas sobre cómo convertirse en un publicador de datos, o si tengo problemas durante la publicación?**

Póngase en contacto con el equipo de Azure Marketplace de hello en < mailto:datamarketbd@microsoft.com > para obtener más información.

