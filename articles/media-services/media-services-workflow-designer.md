---
title: "aaaCreate avanzada codificación flujos de trabajo con el Diseñador de flujo de trabajo | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate había avanzada flujos de trabajo de codificación con el Diseñador de flujo de trabajo."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Creación de flujos de trabajo de codificación avanzada con el Diseñador de flujo de trabajo
## <a name="overview"></a>Información general
Hola **Workflow Designer** es una herramienta de escritorio de Windows que sea utilizados toodesign y generar flujos de trabajo personalizados para la codificación con **flujo de trabajo de Premium de codificación de medios**.
Mediante el uso de potencia de Hola de herramienta del Diseñador de flujo de trabajo hello, puede diseñar y crear flujos de trabajo complejos que se ejecutarán en **Media Encoder Premium**.  

Los flujos de trabajo pueden incluir una lógica de decisión de cliente y realizar una bifurcación en función de propiedades del archivo de origen de entrada de Hola. Puede crear flujos de trabajo con las propiedades overridable y valores dinámicos toomake Hola incluso más complejo codificación tareas fácil toorepeat y personalizar en la nube de Hola.

Entre los flujos de trabajo de ejemplo que puede crear se incluyen:

* Decisión en función de los flujos de trabajo que inspeccionar el contenido de origen de hello para la resolución y codifican pistas de salida de hello deseado solo.  Esto es helfpul mediante la eliminación de pistas de hello desperdiciado que podrían generarse mediante la ampliación de escala Hola origen contenido involuntariamente.
* Varios archivos de entrada pueden ser usado toosupport títulos, superposiciones y combinación contenido junto. 

Esta herramienta también puede ser usado toomodify cualquiera de nuestros [publicados los flujos de trabajo](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> tooget su copia de la herramienta del Diseñador de flujo de trabajo de hello, póngase en contacto con mepd@microsoft.com.
> 
> 

Una vez que creado un archivo de flujo de trabajo, se puede cargar como un activo y, a continuación, usarse para la codificación de archivos multimedia. Para obtener información acerca de cómo tooencode con **flujo de trabajo de Premium de codificación de medios** con **.NET**, consulte [avanzado de codificación con el flujo de trabajo de Premium de codificación de medios](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modificación de flujos de trabajo existentes
Hola predeterminado [publicados los flujos de trabajo](media-services-workflow-designer.md#existing_workflows) puede modificarse mediante la herramienta del Diseñador de Hola. Puede obtener archivos de flujo de trabajo predeterminada de hello [aquí](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). carpeta de Hello también contiene la descripción de Hola de estos archivos.

Hola siguientes vídeos demuestran cómo toouse Hola diseñador.

### <a name="day-1--getting-started"></a>Día 1 – Introducción
El vídeo del día 1 trata de:

* Información general del diseñador
* Flujos de trabajo básicos: "Hello World"
* Creación de varios archivos MP4 de salida para usarlos con streaming de Servicios multimedia de Azure

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Día 2
El vídeo del día 2 trata de:

* Diversos escenarios de archivo de código fuente: control del audio
* Flujos de trabajo con lógica avanzada
* Fases de gráfico

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>Día 3
El vídeo del día 3 trata de:

* Scripting dentro de los flujos de trabajo y planos
* Restricciones con Hola codificador actual
* Preguntas y respuestas

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Paso siguiente
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Si necesita admitir o tiene alguna pregunta sobre la creación de flujos de trabajo personalizados en la herramienta Diseñador de flujo de trabajo de hello, envíe un correo electrónico toomepd@microsoft.com.

## <a name="see-also"></a>Otras referencias
[Azure Premium Encoder Workflow Designer Training Videos (Vídeos de aprendizaje del Diseñador de flujo de trabajo del codificador de Azure Premium)](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

