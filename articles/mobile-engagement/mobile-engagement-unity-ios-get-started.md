---
title: "aaaGet Started with Azure Mobile Engagement para la implementación de iOS de Unity"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para las aplicaciones de Unity implementar dispositivos tooiOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Introducción a Azure Mobile Engagement para la implementación de Unity para iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación de Unity al implementar el dispositivo iOS tooan.
Este tutorial se utiliza Hola clásico Unity poner un tutorial de bola como punto de partida de Hola. Debe seguir los pasos de hello en este [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar con hello integración de Mobile Engagement se muestran en el tutorial de Hola a continuación. 

Este tutorial requiere siguiente de hello:

* [Editor de Unity](http://unity3d.com/get-unity)
* [SDK de Unity para Mobile Engagement](https://aka.ms/azmeunitysdk)
* Editor de XCode

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
### <a name="import-hello-unity-package"></a>Importar paquete de Unity Hola
1. Descargar hello [paquete de Mobile Engagement Unity](https://aka.ms/azmeunitysdk) y lo guarda en la máquina local tooyour. 
2. Vaya demasiado**activos -> Importar paquete -> paquete personalizado** y el paquete de hello seleccione descargado en hello por encima del paso. 
   
    ![][70] 
3. Asegúrese de que se seleccionan todos los archivos y haga clic en el botón **Import** (Importar). 
   
    ![][71] 
4. Una vez que la importación es correcta, verá los archivos SDK de hello importado en el proyecto.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Actualizar hello EngagementConfiguration
1. Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **IOS\_conexión\_cadena** con la cadena de conexión de hello obtenido anteriormente de hello portal de Azure.  
   
    ![][73]
2. Guarde el archivo hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurar la aplicación hello para el seguimiento básico
1. Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición. 
2. Agregue Hola siguiente instrucción using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Agregar Hola después toohello `Start()` (método)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implementar y ejecutar la aplicación hello
1. Conectar una máquina de tooyour de dispositivo de iOS. 
2. Abra **File -> Build Settings** (Archivo -> Configuración de compilación). 
   
    ![][40]
3. Seleccione **iOS** y, después, haga clic en **Switch Platform** (Cambiar plataforma).
   
    ![][41]
   
    ![][42]
4. Haga clic en **Player settings** (Configuración del Reproductor) y proporcione un identificador de agrupación de trabajos válido. 
   
    ![][53]
5. Por último, haga clic en **Build And Run**
   
    ![][54]
6. Es posible que más frecuentes tooprovide un paquete de iOS de carpeta nombre toostore Hola. 
   
    ![][43]
7. Si todo va bien, se compilará el proyecto de Hola y debería abrirlo de en la aplicación de XCode. 
8. Asegúrese de que ese hello **identificador de paquete** es correcto en el proyecto de Hola.  
   
    ![][75]
9. Ahora ejecutar aplicación hello en XCode para que el paquete de hello es dispositivo conectado tooyour implementado y debería ver su juego Unity en su teléfono. 

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
No tiene toodo ninguna configuración adicional en las notificaciones de tooreceive de aplicación y ya está configurado para él.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
