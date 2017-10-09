---
title: "servicio web de aaaTroubleshoot reciclaje un clásico de aprendizaje de máquina de Azure | Documentos de Microsoft"
description: "Identifique y corrija comunes detectó problemas cuando se reciclaje modelo Hola para un servicio Web de aprendizaje de máquina de Azure."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Solución de problemas de hello reciclaje de un servicio Web clásico de aprendizaje de máquina de Azure
## <a name="retraining-overview"></a>Información general sobre reentrenamiento
Cuando se implementa un experimento predictivo, tal como servicio web de puntuación, es un modelo estático. Como los nuevos datos se convierte en disponibles o al consumidor de Hola de hello API tiene sus propios datos, modelo de hello necesita toobe volver a entrenar. 

Para obtener un tutorial completo de hello reciclaje de procesos de un servicio Web clásico, consulte [volver a entrenar máquina aprendizaje modelos mediante programación](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Proceso de reentrenamiento
Cuando necesite tooretrain Hola servicio Web, debe agregar algunos elementos adicionales:

* Un servicio Web que se implementan a partir de hello experimento de entrenamiento. debe tener el experimento de Hello un **resultado del servicio Web** módulo adjunta toohello salida de hello **entrenar modelo** módulo.  
  
    ![Adjuntar Hola salida toohello entrenar modelo para servicios web.][image1]
* Un nuevo extremo agregado tooyour la puntuación del servicio Web.  Puede agregar punto de conexión de hello mediante programación utilizando el código de ejemplo de Hola hace referencia en hello aprendizaje automático de volver a entrenar modelos mediante programación tema o a través de hello portal de Azure clásico.

A continuación, puede usar Hola ejemplo C# código a partir API ayuda página tooretrain modelo del servicio Web de hello entrenamiento. Una vez que se evalúa los resultados de Hola y esté satisfecho con ellas, actualizar modelo entrenado Hola la puntuación del servicio web mediante Hola nuevo punto de conexión que agregó.

Con todas las piezas de hello en su lugar, pasos principales de Hola que debe seguir modelo de hello tooretrain son los siguientes:

1. Llame al servicio Web de aprendizaje de hello: llamada hello es toohello servicio de ejecución de lotes (BES), no Hola servicio de respuesta de solicitud (RR). Puede usar código C# de ejemplo Hola en llamada de API de hello ayuda página toomake Hola. 
2. Buscar valores de hello para hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken*: estos valores se devuelven en la salida de hello desde la Web de aprendizaje de llamada toohello Servicio. 
   ![Mostrar la salida de hello de hello reciclaje hello y muestra los valores de BaseLocation, RelativeLocation y SasBlobToken.][image6]
3. Hola de actualización agrega punto de conexión de Hola la puntuación del servicio web con hello nuevo modelo entrenado: usar código de ejemplo de Hola Hola aprendizaje automático de volver a entrenar modelos mediante programación, actualizar nuevo extremo de hello agregado toohello puntuar modelo con hello recientemente modelo entrenado de hello servicio Web de aprendizaje.

## <a name="common-obstacles"></a>Obstáculos más comunes
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Consulte toosee si tiene Hola corregir la dirección URL de revisión
Hola URL PATCH utilizas debe ser Hola asociado Hola nuevo extremo de puntuación que agregó toohello la puntuación del servicio Web. Hay una serie de formas tooobtain Hola PATCH URL:

**Opción 1: De forma programada**

Hola tooget corríjala PATCH:

1. Ejecute hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de ejemplo.
2. En la salida de hello de AddEndpoint, observa hello *HelpLocation* valor y copie la dirección URL de Hola.
   
   ![HelpLocation en la salida de hello de ejemplo de Hola a addEndpoint.][image2]
3. Pegue la dirección de URL de hello en una página de tooa de toonavigate de explorador que proporciona los vínculos de ayuda para el servicio Web de Hola.
4. Haga clic en hello **recurso de actualización** página de Ayuda de revisión de vínculo tooopen Hola.

**Opción 2: Usar hello portal de Azure clásico**

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Pestaña de aprendizaje automático de hello abierto. ![Pestaña Machine Learning.][image4]
3. Haga clic en el nombre del área de trabajo y, luego, en **Servicios web**.
4. Haga clic en hello la puntuación del servicio Web que está trabajando. (Si no ha modificado el nombre predeterminado de hello del servicio web de hello, termina en [puntuación Exp].)
5. Haga clic en **Agregar extremo**.
6. Después de agrega el punto de conexión de hello, haga clic en el nombre del extremo de Hola. A continuación, haga clic en **recurso de actualización** tooopen Hola página de Ayuda de aplicación de revisiones.

> [!NOTE]
> Si ha agregado Hola extremo toohello servicio Web de aprendizaje en lugar de hello predictivo servicio Web, recibirá el mensaje Hola tras error al hacer clic en hello **recurso de actualización** vínculo: lo sentimos, pero no se admite esta característica o está disponible en este contexto. Este servicio web no tiene ningún recurso actualizable. Nos disculpamos molestias hello y está trabajando en la mejora de este flujo de trabajo.
> 
> 

![Panel del nuevo punto de conexión.][image3]

página de Ayuda de revisión de Hello contiene Hola dirección URL de aplicar la revisión que se debe usar y proporciona código de ejemplo que puede usar toocall lo.

![PATCH URL.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Toosee de comprobación que se está actualizando el extremo de puntuación correcta Hola
* No aplicar la revisión Hola servicio Web de aprendizaje: operación de revisión de hello debe realizarse en hello la puntuación del servicio Web.
* No aplicar la revisión extremo predeterminado de hello en el servicio Web: operación de revisión de hello debe realizarse en Hola de nuevo la puntuación del extremo del servicio Web que agregó.

Puede comprobar qué extremo de hello del servicio Web está activado de hello visitando portal de Azure clásico. 

> [!NOTE]
> Asegúrese de que está agregando Hola extremo toohello predictivo servicio Web, servicio Web de aprendizaje y no Hola. Si ha implementado correctamente un servicio web predictivo y otro de formación, debería ver dos servicios web independientes. Hola predictivo servicio Web debe terminar con "[exp predictiva.]".
> 
> 

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Pestaña de aprendizaje automático de hello abierto. ![Interfaz de usuario del área de trabajo de Machine Learning.][image4]
3. Seleccione su área de trabajo.
4. Haga clic en **Servicios web**.
5. Seleccione su servicio web predictivo.
6. Compruebe que el nuevo punto de conexión se ha agregado el servicio Web de toohello.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Compruebe el área de trabajo de Hola que el servicio web está en tooensure que se encuentra en la región correcta Hola
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Seleccione aprendizaje automático en el menú de Hola.
   ![Interfaz de usuario de la región de Machine Learning.][image4]
3. Compruebe la ubicación de hello del área de trabajo.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
