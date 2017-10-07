---
title: "aaaSet seguridad y el uso Hola API de recomendaciones de aprendizaje de máquina | Documentos de Microsoft"
description: "Preguntas frecuentes de la API de RECOMENDACIONES de Microsoft creada con el aprendizaje automático de Azure"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
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
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Preguntas más frecuentes (P+F) sobre cómo configurar y utilizar la API de recomendaciones de Aprendizaje automático
**¿Qué son las recomendaciones?**

> [!NOTE]
> Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión. Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
> Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)
> 
> 

Para las organizaciones y empresas que se basan en las recomendaciones toocross ventas y productos de subida y los clientes de tootheir de servicios, las recomendaciones de aprendizaje automático de Azure proporciona un motor de recomendaciones de autoservicio. Es una implementación del filtrado de colaboración que usa la factorización matricial como algoritmo básico. Los desarrolladores de aplicaciones pueden tener acceso a recomendaciones mediante las API de REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**¿Qué puedo hacer con las recomendaciones?**

Las recomendaciones toman como entrada un elemento o un conjunto de elementos y devuelven una lista de recomendaciones pertinentes. Por ejemplo, un cliente de un minorista en línea hace clic en un producto. comerciante en línea Hello envía ese producto como entrada tooRECOMMENDATIONS, obtiene una lista de productos de vuelta y decide cuál de estos productos se mostrarán toohello cliente. Es conveniente toouse recomendaciones toooptimize la tienda en línea o incluso tooinform internas center departamento o llamada ventas.

**¿Hay alguna limitación de uso?**

Recomendaciones tiene Hola siguiendo las limitaciones de uso:

* Número máximo de modelos por suscripción: 10
* Número máximo de elementos que puede contener un catálogo: 100.000
* número máximo de Hola de puntos de uso que se mantienen es ~ 5 000 000. Hola más antigua se eliminará si nuevos se cargan o se notificarán.
* El tamaño máximo de datos que puede enviarse por correo electrónico (por ejemplo, importar datos de catálogo o importar datos de uso) es de 200 MB.
* El número de transacciones por segundo (TPS) para una compilación de modelo de Recomendaciones que no está activa es de ~2 TPS. Una compilación de modelo de recomendaciones que está activa puede contener una too20 TPS.

## <a name="purchase-and-billing"></a>Compra y facturación
**¿Cuánto cuesta recomendaciones durante el período de inicio de hello?**

Las recomendaciones son un servicio basado en suscripción. El pago se realiza en función del volumen de transacciones al mes. Puede comprobar hello [ofrecen página](https://datamarket.azure.com/dataset/amla/recommendations) en Microsoft Azure Marketplace para obtener más información.

**¿Hay algún coste asociado al seguimiento de las recomendaciones o al almacenamiento de la actividad del usuario?**

No en el momento de Hola.

**¿Tienen las recomendaciones una prueba gratuita?**

Hay una prueba gratuita que está restringido too10, 000 transacciones al mes.

**¿Cuánto se me facturará por las recomendaciones?**

Una suscripción de pago es cualquier suscripción para la que hay que pagar una cuota mensual. Al adquirir una suscripción de pago, se le cobrará inmediatamente para hello primero uso del mes. Se le cobrará la cantidad de Hola que está asociado con la oferta de hello en la página de suscripción de hello (más los impuestos aplicables). Este cargo mensual se realiza cada mes en hello mismo calendario fecha de compra original hasta que cancele la suscripción de Hola. 

**¿Cómo puedo actualizar servicio de nivel superior de tooa?**

También puede comprar o actualizar su suscripción de hello [ofrecen página](https://datamarket.azure.com/dataset/amla/recommendations) página de Microsoft Azure Marketplace.

Al actualizar una suscripción:

* Las transacciones que permanecen en su suscripción anterior no se agregan tooyour nueva suscripción. 
* Pagar el precio completo para nueva suscripción de hello, incluso aunque tenga transacciones sin utilizar en su suscripción anterior.

Proceso tooupgrade una suscripción:

* Nevigate toohello [ofrecen página](https://datamarket.azure.com/dataset/amla/recommendations).
* Inicie sesión en Marketplace toohello si ya no has iniciado sesión.
* En el panel derecho de hello, se muestran todos los planes disponibles Hola. Haga clic en el botón de opción de Hola para plan de Hola que usted quiera tooupgrade a.
* Si desea tooupgrade, haga clic en **Aceptar**. Si no desea tooupgrade, haga clic en **cancelar**.

**Importante** aparece el cuadro de diálogo Hola leer detenidamente antes de realizar la actualización porque hay implicaciones de facturación y uso.

**¿Si va a finalizar tooRecommendations de mi suscripción?**

La suscripción finalizará cuando la cancele. Si desea que toocancel sus suscripciones, vea Hola siguiendo las instrucciones.

**¿Cómo cancelo mi suscripción a las recomendaciones?**

toocancel su suscripción, Hola uso siguiendo los pasos. Si su suscripción actual es una suscripción de pago, la suscripción sigue en vigor hasta el final de Hola de hello período de facturación actual. Si necesita hello toobe cancelación efectivo inmediatamente, póngase en contacto con nosotros en [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Tenga en cuenta** no se proporciona ningún reembolso por cancelaciones anteriores final de Hola de un período de facturación o por transacciones no utilizadas en un período de facturación.

* Navegue toohello [ofrecen página](https://datamarket.azure.com/dataset/amla/recommendations).
* Inicie sesión en Marketplace toohello si ya no has iniciado sesión.
* Haga clic en **cancelar** toohello derecha del nombre del conjunto de datos de Hola y el estado. También puede utilizar esta suscripción hasta llegar Hola final del programa Hola a un punto o el límite de transacciones de facturación actual (lo que ocurra primero).

Si desea que toocancel la suscripción inmediatamente por lo que puede adquirir una nueva suscripción, presentar una incidencia en [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Introducción a las recomendaciones
**¿Me van a servir las recomendaciones?** 

Recomendaciones de aprendizaje automático es para las organizaciones y empresas que se basan en recomendaciones toocross ventas y venda productos o servicios tootheir los clientes. Si tiene un sitio web orientado a clientes, personal de ventas, un equipo de ventas interno o un centro de llamadas y si, además, ofrece un catálogo con varias docenas de productos o servicios, su balance final puede beneficiarse de usar estas recomendaciones. 

Experimentar con las recomendaciones es toobe diseñada bastante simple. versión actual basadas en la API de Hello requiere conocimientos básicos de programación. Si necesita ayuda, póngase en contacto con el fabricante de Hola que desarrolló el sitio Web. Si tiene un departamento de TI interno o un desarrollador interno, deben ser capaz de tooget toowork de recomendaciones para usted. 

**¿Cuáles son los requisitos previos de Hola para configurar recomendaciones?**

Recomendaciones requiere que haya un registro de las opciones de usuario tal y como se relaciona con el catálogo de tooyour. Si no dispone de un registro de este tipo y cuenta con un sitio web orientado al cliente, las recomendaciones pueden recopilar la actividad de los usuarios por usted. 

Las recomendaciones también requieren un catálogo de sus productos o servicios. Si no tienes catálogo hello, recomendaciones pueden usar datos de uso reales de los clientes de Hola y refinar un catálogo. Un catálogo "implícito" no incluirá artículos que no estaban "notificados" como parte de transacciones de usuario.

**¿Cómo configuro recomendaciones para hello primera vez?**

Después de [suscripción](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, debe usar documentación de API de Hola Hola [recomendaciones de aprendizaje de máquina de Azure - Guía de inicio rápido](machine-learning-recommendation-api-quick-start-guide.md) tooset servicio Hola.

**¿Dónde puedo encontrar documentación de API?** 

documentación de la API de Hello es [recomendaciones de aprendizaje de máquina de Azure-Guía de inicio rápido](machine-learning-recommendation-api-quick-start-guide.md).

**¿Qué opciones tengo tooRecommendations de datos de catálogo y el uso de tooupload?**

Tiene dos opciones para cargar los datos de uso y catálogo: puede exportar datos de Hola de su sistema CRM o en otros registros y cargarlo tooRecommendations, o puede agregar sitio Web de tooyour de etiquetas que realizará el seguimiento de las actividades del usuario. Si utiliza este último método de hello, se almacenarán datos de hello en Azure.

## <a name="maintenance-and-support"></a>Mantenimiento y soporte técnico
**¿Qué volumen pueden tener mis datos?**

Cada conjunto de datos puede contener too100, 000 elementos del catálogo e instalación too2048 MB de datos de uso.
Además, una suscripción puede contener hasta conjuntos de datos too10 (modelos).

**¿Dónde puedo obtener soporte técnico para las recomendaciones?**

El soporte técnico está disponible en hello [soporte técnico de Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) sitio.

**¿Dónde puedo encontrar los términos de Hola de uso?**

[Términos de uso de la API de recomendaciones de Aprendizaje automático de Microsoft Azure](https://datamarket.azure.com/dataset/amla/recommendations#terms).

