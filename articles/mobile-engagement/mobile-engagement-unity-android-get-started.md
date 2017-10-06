---
title: "aaaGet Started with Azure Mobile Engagement para Android Unity implementación"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para las aplicaciones de Unity implementar dispositivos tooiOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Introducción a Azure Mobile Engagement para la implementación de Unity para Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación de Unity al implementar el dispositivo Android tooan.
Este tutorial se utiliza Hola clásico Unity poner un tutorial de bola como punto de partida de Hola. Debe seguir los pasos de hello en este [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar con hello integración de Mobile Engagement se muestran en el tutorial de Hola a continuación. 

Este tutorial requiere siguiente de hello:

* [Editor de Unity](http://unity3d.com/get-unity)
* [SDK de Unity para Mobile Engagement](https://aka.ms/azmeunitysdk)
* SDK de Google Android

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Android
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
1. Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **ANDROID\_conexión\_cadena** con cadena de conexión de hello obtuvo versiones anteriores de hello portal de Azure.  
   
    ![][73]
2. Guardar archivo hello 
3. Ejecute **File -> Engagement -> Generate Android Manifest** (Archivo -> Interacción - > Generar manifiesto Android). Se trata de complemento de hello agregada por hello SDK de Mobile Engagement y haga clic en ella se actualizará automáticamente la configuración del proyecto. 
   
    ![][74]

> [!IMPORTANT]
> Hacerlo seguro tooexecute cada vez que actualice hello **EngagementConfiguration** archivo lo contrario no se reflejarán los cambios en la aplicación hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurar la aplicación hello para el seguimiento básico
1. Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición. 
2. Agregue Hola siguiente instrucción using:
   
        using Microsoft.Azure.Engagement.Unity;
3. Agregar Hola después toohello `Start()` (método)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implementar y ejecutar la aplicación hello
Asegúrese de que tiene instalados en su equipo antes de intentar toodeploy este dispositivo de tooyour de aplicación de Unity de SDK de Android. 

1. Conectar una máquina de tooyour dispositivo Android. 
2. Abra **File -> Build Settings** (Archivo -> Configuración de compilación). 
   
    ![][40]
3. Seleccione **Android** y, después, haga clic en **Switch Platform** (Cambiar plataforma).
   
    ![][51]
   
    ![][52]
4. Haga clic en **Player settings** (Configuración del Reproductor) y proporcione un identificador de agrupación de trabajos válido. 
   
    ![][53]
5. Por último, haga clic en **Build And Run**
   
    ![][54]
6. Es posible que más frecuentes tooprovide un paquete carpeta nombre toostore Hola Android. 
7. Si todo va bien, paquetes de saludo será implementado tooyour conectado dispositivo y se debería aparecer su juego Unity en su teléfono. 

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Actualizar hello EngagementConfiguration
1. Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **ANDROID\_GOOGLE\_número** con hello **proyecto de Google Número** obtenido anteriormente desde el portal para desarrolladores de nube de Google Hola. Se trata de una cadena de valor por lo que debe tooenclose seguro en comillas dobles. 
   
    ![][75]
2. Guarde el archivo hello. 
3. Ejecute **File -> Engagement -> Generate Android Manifest** (Archivo -> Interacción - > Generar manifiesto Android). Se trata de complemento de hello agregada por hello SDK de Mobile Engagement y haga clic en ella se actualizará automáticamente la configuración del proyecto. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Configurar notificaciones de tooreceive aplicación Hola
1. Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición. 
2. Agregar Hola después toohello `Start()` (método)
   
        EngagementReachAgent.Initialize();
3. Ahora que hello aplicación se actualiza, implemente y ejecute la aplicación hello en un dispositivo por instrucciones de hello proporcionadas a continuación. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
