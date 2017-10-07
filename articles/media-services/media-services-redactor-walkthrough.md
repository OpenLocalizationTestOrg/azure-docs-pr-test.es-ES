---
title: "aaaRedact caras con el tutorial de análisis de multimedia de Azure | Documentos de Microsoft"
description: "En este tema se muestra instrucciones paso a paso acerca de cómo toorun un flujo de trabajo de redacción completa mediante el Explorador de servicios multimedia de Azure (AMSE) y Azure Media Redactor visualizador (herramienta de código abierto)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Tutorial de censura de rostros con Azure Media Analytics

## <a name="overview"></a>Información general

**Redactor de Azure Media** es un [análisis de multimedia de Azure](media-services-analytics-overview.md) procesador multimedia (MP) que ofrece la redacción de cara escalable en la nube de Hola. Redacción de cara permite toomodify el vídeo en caras de tooblur de orden de los usuarios seleccionados. Puede desear toouse Hola el servicio de redacción de cara en escenarios de seguridad y medios de noticias públicos. Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con esta imagen de hello servicio proceso de redacción requiere unos pocos pasos sencillos. Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).

Para obtener más información acerca de **Redactor de multimedia de Azure**, vea hello [información general de redacción de cara](media-services-face-redaction.md) tema.

En este tema se muestra instrucciones paso a paso acerca de cómo toorun un flujo de trabajo de redacción completa mediante el Explorador de servicios multimedia de Azure (AMSE) y Azure Media Redactor visualizador (herramienta de código abierto).

Hola **Redactor de multimedia de Azure** MP está actualmente en vista previa. Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos. Actualmente, esta versión preliminar es gratuita. En la versión actual de hello, hay un límite de 10 minutos en la duración del vídeo procesado.

Para más información, consulte [este blog](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) .

## <a name="azure-media-services-explorer-workflow"></a>Flujo de trabajo del Explorador de Azure Media Services

Hello tooget de manera más fácil trabajar con Redactor es la herramienta de AMSE de código abierto toouse hello en github. Puede ejecutar un flujo de trabajo simplificado a través de **combinan** modo si no necesita acceso toohello anotación json o hello cara imágenes jpg.

### <a name="download-and-setup"></a>Descarga e instalación

1. Herramienta de AMSE Hola descargar [aquí](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Inicie sesión en tooyour cuenta de servicios multimedia mediante la clave del servicio.

    tooobtain Hola nombre de cuenta y la información de clave, vaya toohello [portal de Azure](https://portal.azure.com/) y seleccione su cuenta de AMS. A continuación, seleccione Configuración > Claves. ventanas de Hello administrar claves muestra el nombre de la cuenta de hello y claves primarias y secundarias de Hola se muestra. Copiar valores de nombre de la cuenta de Hola y Hola primary key.

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Primer paso: Modo Analizar

1. Cargue el archivo multimedia a través de Activo – > Cargar, o bien arrástrelo y suéltelo. 
1. Haga clic en el botón derecho y procese el archivo multimedia utilizando Análisis multimedia > Azure Media Redactor – > Modo Analizar. 


![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

salida de Hello incluirá un archivo json de anotaciones con datos de ubicación de fuente, así como un jpg de cada tipo detectado. 

![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Segundo paso: Modo Redact (Censurar)

1. Cargue su toohello de recurso de vídeo original de salida desde la primera pasada de Hola y establecer como un recurso principal. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Opcional) Cargar un archivo de 'Dance_idlist.txt' que incluye una lista de nueva línea delimitada de identificadores que se va tooredact hello. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Opcional) Asegúrese de cualquier archivo de annotations.json toohello modificaciones, tal como aumentar Hola límites del cuadro de límite. 
4. Haga clic Hola activo de salida desde la primera pasada de hello, seleccionar Hola Redactor y ejecutar con hello **Redact** modo. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Para descargar o compartirlos Hola salida redactado final activo. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Herramienta de código abierto Azure Media Redactor Visualizer

Un código abierto [herramienta visualizador](https://github.com/Microsoft/azure-media-redactor-visualizer) es toohelp diseñada a los desarrolladores iniciándose con formato de anotaciones de hello con salida de hello y análisis.

Después de clonar el repositorio de hello, en el proyecto de orden toorun hello, necesitará toodownload FFMPEG desde su [sitio oficial](https://ffmpeg.org/download.html).

Si es un desarrollador que trate de hello tooparse dato de anotación de JSON, buscar dentro de Models.MetaData para obtener ejemplos de código de ejemplo.

### <a name="set-up-hello-tool"></a>Configurar la herramienta de Hola

1.  Descargue y generar solución completa de Hola. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Descargue FFMPEG desde [aquí](https://ffmpeg.org/download.html). Este proyecto se desarrolló originalmente mediante la versión be1d324 (2016-10-04) con vinculación estática. 
3.  Copie ffmpeg.exe y ffprobe.exe toohello misma carpeta de salida como AzureMediaRedactor.exe. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Ejecute AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Usar la herramienta Hola

1. Procesar sus vídeos en su cuenta de servicios multimedia de Azure con hello Redactor MP en modo de analizar. 
2. Descargar archivo de vídeo original de Hola y de salida de hello de redacción de hello: analizar el trabajo. 
3. Ejecutar la aplicación del visualizador de hello y elija archivos Hola anteriores. 

    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Obtenga una vista previa del archivo. Seleccione cara le gustaría tooblur a través de la barra lateral de hello en hello derecho. 
    
    ![Censura de rostros](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  campo de texto de Hello inferior se actualizará con la cara Hola identificadores. Cree un archivo denominado "idlist.txt" con estos identificadores como una lista delimitada de nueva línea. 

    >[!NOTE]
    > Hola idlist.txt debe guardarse en ANSI. Puede utilizar el Bloc de notas toosave en ANSI.
    
6.  Cargar este recurso de salida de archivo toohello del paso 1. Cargar activo original de vídeo toothis Hola así y establecer como elemento principal. 
7.  Ejecutar trabajo de redacción de este recurso con "Redact" modo tooget Hola redactado vídeo final. 

## <a name="next-steps"></a>Pasos siguientes 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

[Demostraciones de Análisis multimedia de Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Anuncio de función de censura facial para Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/)
