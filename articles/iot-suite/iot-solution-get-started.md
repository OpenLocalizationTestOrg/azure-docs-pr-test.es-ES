---
title: "Ejemplo de IoT de Azure MyDriving: inicio rápido | Microsoft Docs"
description: "Empezar a trabajar con una aplicación que es una demostración completa de cómo tooarchitect un sistema IoT mediante Microsoft Azure, incluido el análisis de transmisiones, aprendizaje automático y concentradores de eventos."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>Sistema IoT de MyDriving: inicio rápido
MyDriving es un sistema que se muestra hello diseño e implementación de una típica [Internet de las cosas](iot-suite-overview.md) solución (IoT) que recopila telemetría de dispositivos, procesa esos datos en la nube de Hola y se aplica el aprendizaje automático tooprovide una respuesta adaptable. demostración de Hello registra datos sobre los viajes en su coche, mediante el uso de datos de su teléfono móvil y un adaptador que recopila información del sistema de control de su automóvil. Utiliza esta información de tooprovide de datos de su estilo determinante en los usuarios de tooother de comparación.

Hola real de MyDriving sirve tooget iniciado para crear su propia solución de IoT. Pero antes de eso, vamos a comenzar a dar con hello MyDriving propia aplicación, como un miembro de nuestro equipo de usuario de prueba. Esto proporciona una experiencia de aplicación hello y sistema de hello detrás de él como un consumidor, antes de profundizar en arquitectura de Hola. También presenta tooHockeyApp, una manera de administrar las distribuciones de alfa y beta de Hola de los usuarios de aplicaciones tootest frío.

## <a name="use-hello-mobile-experience"></a>Usar la experiencia móvil de Hola
Puede usar hello MyDriving aplicación si tienes un dispositivo Android, iOS o Windows 10.

### <a name="android-and-windows-10-mobile-installation"></a>Instalación de Android y Windows 10 Mobile
En su dispositivo:

1. Dé permiso a las aplicaciones de desarrollo:
   
   * Android: en **Ajustes** > **Seguridad**, dé permiso a las aplicaciones de **orígenes desconocidos**.
   * Windows 10: en **Configuración** > **Actualizaciones** > **Para desarrolladores**, establezca **Modo de programador**.
2. Únase a nuestro equipo de prueba beta mediante el registro o el inicio de sesión en [HockeyApp](https://rink.hockeyapp.net). HockeyApp resulta fácil toodistribute primeras versiones de los usuarios de tootest de aplicación.
   
   Si usa Windows 10, utilice Explorador de Edge Hola.
   
   Si eres un asistente de compilación 2016, inicie sesión con hello mismo correo electrónico de la cuenta de Microsoft que se registró para la conferencia de hello, mediante uno de hello botones de Microsoft. Ya está registrado en HockeyApp.
   
   ![Pantalla de inicio de sesión de HockeyApp](./media/iot-solution-get-started/image1.png)
3. Descargue e instale la aplicación hello desde aquí:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Hay dos elementos. Instalar certificado de hello en **personas de confianza**. A continuación, instale la aplicación hello.

*¿Problemas de iniciar la aplicación hello en Windows 10 Mobile?* Puede ser que el teléfono tenga pendientes una o dos actualizaciones. Asegúrese de que tiene las actualizaciones más recientes de hello, o instalar:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Instalación para iOS
Si a la que asistió 2016 de compilación, descargar aplicación hello como un miembro de nuestro equipo de prueba en HockeyApp:

1. En el dispositivo iOS, inicie sesión demasiado[HockeyApp](https://rink.hockeyapp.net).
   Use uno de hello botones de inicio de sesión de Microsoft e inicie sesión en con Hola mismo correo de la cuenta de Microsoft que se ha registrado con la conferencia de Hola. (No utilice los campos de correo electrónico y la contraseña de hello).
   
   ![Pantalla de inicio de sesión de HockeyApp](./media/iot-solution-get-started/image1.png)
2. En el panel de HockeyApp hello, seleccione MyDriving y descargarla.
3. Autorizar la versión beta de Hola de HockeyApp:
   
   a. Vaya demasiado**configuración** > **General** > **perfiles y la administración de dispositivos.**
   
   b. Confiar en hello **bits estadio GmbH** certificado.

Si no asistió 2016 de compilación, puede compilar e implementar la aplicación hello usted mismo:

1. Descargar código de hello [desde GitHub].
2. Realice la compilación e implementación [con Xamarin].

Obtener más información en hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Obtención de un adaptador OBD (opcional)
Esto forma parte de Hola que esto hace que un sistema de Internet de las cosas real. Puede usar la aplicación hello sin un controlador, pero es más divertida con algo real de hello y no son costosas.

Diagnóstico a bordo (DAB) es la característica de Hola de su automóvil que Hola artículos usa tootune su automóvil y diagnosticar ruidos impares y luces de advertencia. A menos que sea su automóvil de antigüedad de excelente, encontrará un socket en alguna parte en la cabina de hello, normalmente detrás de un paso de la rueda en el panel de Hola. Con el conector de derecho de hello, puede obtener las métricas de rendimiento del motor de Hola y realizar algunos ajustes. Un conector de DAB puede adquirirse económica desde sitios de saludo habitual. Se conecta mediante la aplicación de tooan Bluetooth o Wi-Fi en el teléfono.

En este caso, vamos tooconnect la nube de toohello automóvil. conexión directa de Hola de hello DAB es tooyour teléfono, pero nuestra aplicación funciona como una retransmisión. Telemetría de su automóvil se enviará recta toohello MyDriving IoT hub, donde resulta procesará toolog los viajes y a evaluar su estilo de conducir.

tooconnect un dispositivo DAB:

1. Compruebe que su automóvil tenga un socket OBD.
2. Obtenga un adaptador OBD.
   
   * Si está usando un teléfono Android o Windows, necesita un adaptador OBD II compatible con Bluetooth. Usamos la [herramienta de análisis BAFX Products 34t5 Bluetooth OBDII].
   * Si está usando un teléfono iOS, necesitará un adaptador OBD habilitado para Wi-Fi. Usamos el [detector de diagnóstico y adaptador OBD ScanTool OBDLink MX Wi-Fi].
3. Siga las instrucciones de Hola que vienen con su tooconnect de adaptador DAB se tooyour teléfono. Tenga en cuenta los siguiente de hello:
   
   * Un adaptador Bluetooth debe estar emparejado con teléfono hello, hello **configuración** página.
   * Un adaptador de Wi-Fi debe tener una dirección de hello intervalo 192.168.
4. Si tiene varios automóviles, puede conseguir un adaptador independiente para cada uno de ellos (un máximo de tres).

Si no tiene un adaptador de DAB, aplicación hello todavía enviará datos de velocidad de toohello de receptor GPS del teléfono Hola volver y la ubicación finalicen y le preguntará si desea toosimulate una DAB.

Puede encontrar más información acerca de la aplicación hello usa datos de adaptador de DAB hello y opciones para crear su propio dispositivo DAB en sección 2.1, "Dispositivos de IoT" Hola [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Usar una aplicación Hola
Inicie la aplicación hello. Hay un toowalk inicial de inicio rápido le guían a través de su funcionamiento.

### <a name="track-your-trips"></a>Realice el seguimiento de sus viajes.
Puntee en hello botón registro (big círculo rojo en la parte inferior de Hola de pantalla de bienvenida) toostart un viaje y, nuevo en tooend.

![Ilustración del botón de registro de hello para el seguimiento de ida y vuelta](./media/iot-solution-get-started/image2.png)

Cada vez que inicie un recorrido, si no hay ningún dispositivo DAB, se le preguntará si desea que el simulador de hello toouse.

Al final de Hola de un recorrido, botón de detención de derivación de Hola y obtener un resumen.

![Ejemplo de un resumen de viaje](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Revise sus viajes.
![Ejemplo de un viaje anterior](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Revise su perfil.
![Ejemplo de un perfil de conducción](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Envíenos sus comentarios de prueba.
Ya hemos creado el punto de partida de MyDriving toohelp sus propios sistemas de IoT, por supuesto, es deseable toohear del usuario acerca de cómo funciona. Queremos saber si:

* Se enfrenta a dificultades y desafíos.
* Hay un punto de extensión que le resulte más conveniente escenario tooyour.
* Buscar un tooaccomplish de manera más eficaz de ciertas necesidades.
* Tiene cualquier sugerencia para mejorar MyDriving o esta documentación.

Dentro de hello MyDriving propia aplicación, puede usar mecanismo de comentarios de Hola integrado HockeyApp: en iOS y Android, simplemente asigne su teléfono un apretón o usar hello **comentarios** comando de menú. Esta acción asociará automáticamente una captura de pantalla, por lo que ya sabremos de que está hablando. Y si hay cualquier bloqueos indeseable, HockeyApp recopila Hola bloqueo registros tootell nos sobre ellos. También puede proporcionar comentarios a través de hello [HockeyApp portal].

Asimismo puede registrar un [problema en GitHub] o dejar un comentario a continuación (edición en inglés).

¡Esperamos tener toohearing del usuario.

## <a name="next-steps"></a>Pasos siguientes
* Explorar hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs) toounderstand cómo hemos diseñado y compilado Hola MyDriving todo el sistema.
* [Cree e implemente un sistema por su cuenta](iot-solution-build-system.md) con nuestros scripts de Azure Resource Manager. Hola [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs) también le guía a través de las áreas donde realizará Hola mayoría de las personalizaciones.

[desde GitHub]: https://github.com/Azure-Samples/MyDriving
[con Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[herramienta de análisis BAFX Products 34t5 Bluetooth OBDII]: http://www.amazon.com/gp/product/B005NLQAHS
[detector de diagnóstico y adaptador OBD ScanTool OBDLink MX Wi-Fi]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problema en GitHub]: https://github.com/Azure-Samples/MyDriving/issues
