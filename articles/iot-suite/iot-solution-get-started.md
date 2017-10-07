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
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="e5066-103">Sistema IoT de MyDriving: inicio rápido</span><span class="sxs-lookup"><span data-stu-id="e5066-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="e5066-104">MyDriving es un sistema que se muestra hello diseño e implementación de una típica [Internet de las cosas](iot-suite-overview.md) solución (IoT) que recopila telemetría de dispositivos, procesa esos datos en la nube de Hola y se aplica el aprendizaje automático tooprovide una respuesta adaptable.</span><span class="sxs-lookup"><span data-stu-id="e5066-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="e5066-105">demostración de Hello registra datos sobre los viajes en su coche, mediante el uso de datos de su teléfono móvil y un adaptador que recopila información del sistema de control de su automóvil.</span><span class="sxs-lookup"><span data-stu-id="e5066-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="e5066-106">Utiliza esta información de tooprovide de datos de su estilo determinante en los usuarios de tooother de comparación.</span><span class="sxs-lookup"><span data-stu-id="e5066-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="e5066-107">Hola real de MyDriving sirve tooget iniciado para crear su propia solución de IoT.</span><span class="sxs-lookup"><span data-stu-id="e5066-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="e5066-108">Pero antes de eso, vamos a comenzar a dar con hello MyDriving propia aplicación, como un miembro de nuestro equipo de usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="e5066-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="e5066-109">Esto proporciona una experiencia de aplicación hello y sistema de hello detrás de él como un consumidor, antes de profundizar en arquitectura de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5066-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="e5066-110">También presenta tooHockeyApp, una manera de administrar las distribuciones de alfa y beta de Hola de los usuarios de aplicaciones tootest frío.</span><span class="sxs-lookup"><span data-stu-id="e5066-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="e5066-111">Usar la experiencia móvil de Hola</span><span class="sxs-lookup"><span data-stu-id="e5066-111">Use hello mobile experience</span></span>
<span data-ttu-id="e5066-112">Puede usar hello MyDriving aplicación si tienes un dispositivo Android, iOS o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e5066-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="e5066-113">Instalación de Android y Windows 10 Mobile</span><span class="sxs-lookup"><span data-stu-id="e5066-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="e5066-114">En su dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e5066-114">On your device:</span></span>

1. <span data-ttu-id="e5066-115">Dé permiso a las aplicaciones de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="e5066-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="e5066-116">Android: en **Ajustes** > **Seguridad**, dé permiso a las aplicaciones de **orígenes desconocidos**.</span><span class="sxs-lookup"><span data-stu-id="e5066-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="e5066-117">Windows 10: en **Configuración** > **Actualizaciones** > **Para desarrolladores**, establezca **Modo de programador**.</span><span class="sxs-lookup"><span data-stu-id="e5066-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="e5066-118">Únase a nuestro equipo de prueba beta mediante el registro o el inicio de sesión en [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="e5066-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="e5066-119">HockeyApp resulta fácil toodistribute primeras versiones de los usuarios de tootest de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5066-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="e5066-120">Si usa Windows 10, utilice Explorador de Edge Hola.</span><span class="sxs-lookup"><span data-stu-id="e5066-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="e5066-121">Si eres un asistente de compilación 2016, inicie sesión con hello mismo correo electrónico de la cuenta de Microsoft que se registró para la conferencia de hello, mediante uno de hello botones de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5066-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="e5066-122">Ya está registrado en HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="e5066-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Pantalla de inicio de sesión de HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="e5066-124">Descargue e instale la aplicación hello desde aquí:</span><span class="sxs-lookup"><span data-stu-id="e5066-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="e5066-125">Android</span><span class="sxs-lookup"><span data-stu-id="e5066-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="e5066-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e5066-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="e5066-127">Hay dos elementos.</span><span class="sxs-lookup"><span data-stu-id="e5066-127">There are two items.</span></span> <span data-ttu-id="e5066-128">Instalar certificado de hello en **personas de confianza**.</span><span class="sxs-lookup"><span data-stu-id="e5066-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="e5066-129">A continuación, instale la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e5066-129">Then install hello app.</span></span>

<span data-ttu-id="e5066-130">*¿Problemas de iniciar la aplicación hello en Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="e5066-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="e5066-131">Puede ser que el teléfono tenga pendientes una o dos actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="e5066-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="e5066-132">Asegúrese de que tiene las actualizaciones más recientes de hello, o instalar:</span><span class="sxs-lookup"><span data-stu-id="e5066-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="e5066-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="e5066-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="e5066-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="e5066-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="e5066-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="e5066-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="e5066-136">Instalación para iOS</span><span class="sxs-lookup"><span data-stu-id="e5066-136">iOS installation</span></span>
<span data-ttu-id="e5066-137">Si a la que asistió 2016 de compilación, descargar aplicación hello como un miembro de nuestro equipo de prueba en HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="e5066-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="e5066-138">En el dispositivo iOS, inicie sesión demasiado[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="e5066-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="e5066-139">Use uno de hello botones de inicio de sesión de Microsoft e inicie sesión en con Hola mismo correo de la cuenta de Microsoft que se ha registrado con la conferencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5066-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="e5066-140">(No utilice los campos de correo electrónico y la contraseña de hello).</span><span class="sxs-lookup"><span data-stu-id="e5066-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Pantalla de inicio de sesión de HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="e5066-142">En el panel de HockeyApp hello, seleccione MyDriving y descargarla.</span><span class="sxs-lookup"><span data-stu-id="e5066-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="e5066-143">Autorizar la versión beta de Hola de HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="e5066-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="e5066-144">a.</span><span class="sxs-lookup"><span data-stu-id="e5066-144">a.</span></span> <span data-ttu-id="e5066-145">Vaya demasiado**configuración** > **General** > **perfiles y la administración de dispositivos.**</span><span class="sxs-lookup"><span data-stu-id="e5066-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="e5066-146">b.</span><span class="sxs-lookup"><span data-stu-id="e5066-146">b.</span></span> <span data-ttu-id="e5066-147">Confiar en hello **bits estadio GmbH** certificado.</span><span class="sxs-lookup"><span data-stu-id="e5066-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="e5066-148">Si no asistió 2016 de compilación, puede compilar e implementar la aplicación hello usted mismo:</span><span class="sxs-lookup"><span data-stu-id="e5066-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="e5066-149">Descargar código de hello [desde GitHub].</span><span class="sxs-lookup"><span data-stu-id="e5066-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="e5066-150">Realice la compilación e implementación [con Xamarin].</span><span class="sxs-lookup"><span data-stu-id="e5066-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="e5066-151">Obtener más información en hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="e5066-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="e5066-152">Obtención de un adaptador OBD (opcional)</span><span class="sxs-lookup"><span data-stu-id="e5066-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="e5066-153">Esto forma parte de Hola que esto hace que un sistema de Internet de las cosas real.</span><span class="sxs-lookup"><span data-stu-id="e5066-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="e5066-154">Puede usar la aplicación hello sin un controlador, pero es más divertida con algo real de hello y no son costosas.</span><span class="sxs-lookup"><span data-stu-id="e5066-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="e5066-155">Diagnóstico a bordo (DAB) es la característica de Hola de su automóvil que Hola artículos usa tootune su automóvil y diagnosticar ruidos impares y luces de advertencia.</span><span class="sxs-lookup"><span data-stu-id="e5066-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="e5066-156">A menos que sea su automóvil de antigüedad de excelente, encontrará un socket en alguna parte en la cabina de hello, normalmente detrás de un paso de la rueda en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5066-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="e5066-157">Con el conector de derecho de hello, puede obtener las métricas de rendimiento del motor de Hola y realizar algunos ajustes.</span><span class="sxs-lookup"><span data-stu-id="e5066-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="e5066-158">Un conector de DAB puede adquirirse económica desde sitios de saludo habitual.</span><span class="sxs-lookup"><span data-stu-id="e5066-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="e5066-159">Se conecta mediante la aplicación de tooan Bluetooth o Wi-Fi en el teléfono.</span><span class="sxs-lookup"><span data-stu-id="e5066-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="e5066-160">En este caso, vamos tooconnect la nube de toohello automóvil.</span><span class="sxs-lookup"><span data-stu-id="e5066-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="e5066-161">conexión directa de Hola de hello DAB es tooyour teléfono, pero nuestra aplicación funciona como una retransmisión.</span><span class="sxs-lookup"><span data-stu-id="e5066-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="e5066-162">Telemetría de su automóvil se enviará recta toohello MyDriving IoT hub, donde resulta procesará toolog los viajes y a evaluar su estilo de conducir.</span><span class="sxs-lookup"><span data-stu-id="e5066-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="e5066-163">tooconnect un dispositivo DAB:</span><span class="sxs-lookup"><span data-stu-id="e5066-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="e5066-164">Compruebe que su automóvil tenga un socket OBD.</span><span class="sxs-lookup"><span data-stu-id="e5066-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="e5066-165">Obtenga un adaptador OBD.</span><span class="sxs-lookup"><span data-stu-id="e5066-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="e5066-166">Si está usando un teléfono Android o Windows, necesita un adaptador OBD II compatible con Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="e5066-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="e5066-167">Usamos la [herramienta de análisis BAFX Products 34t5 Bluetooth OBDII].</span><span class="sxs-lookup"><span data-stu-id="e5066-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="e5066-168">Si está usando un teléfono iOS, necesitará un adaptador OBD habilitado para Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="e5066-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="e5066-169">Usamos el [detector de diagnóstico y adaptador OBD ScanTool OBDLink MX Wi-Fi].</span><span class="sxs-lookup"><span data-stu-id="e5066-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="e5066-170">Siga las instrucciones de Hola que vienen con su tooconnect de adaptador DAB se tooyour teléfono.</span><span class="sxs-lookup"><span data-stu-id="e5066-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="e5066-171">Tenga en cuenta los siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e5066-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="e5066-172">Un adaptador Bluetooth debe estar emparejado con teléfono hello, hello **configuración** página.</span><span class="sxs-lookup"><span data-stu-id="e5066-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="e5066-173">Un adaptador de Wi-Fi debe tener una dirección de hello intervalo 192.168.</span><span class="sxs-lookup"><span data-stu-id="e5066-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="e5066-174">Si tiene varios automóviles, puede conseguir un adaptador independiente para cada uno de ellos (un máximo de tres).</span><span class="sxs-lookup"><span data-stu-id="e5066-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="e5066-175">Si no tiene un adaptador de DAB, aplicación hello todavía enviará datos de velocidad de toohello de receptor GPS del teléfono Hola volver y la ubicación finalicen y le preguntará si desea toosimulate una DAB.</span><span class="sxs-lookup"><span data-stu-id="e5066-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="e5066-176">Puede encontrar más información acerca de la aplicación hello usa datos de adaptador de DAB hello y opciones para crear su propio dispositivo DAB en sección 2.1, "Dispositivos de IoT" Hola [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="e5066-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="e5066-177">Usar una aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="e5066-177">Use hello app</span></span>
<span data-ttu-id="e5066-178">Inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e5066-178">Start hello app.</span></span> <span data-ttu-id="e5066-179">Hay un toowalk inicial de inicio rápido le guían a través de su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="e5066-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="e5066-180">Realice el seguimiento de sus viajes.</span><span class="sxs-lookup"><span data-stu-id="e5066-180">Track your trips</span></span>
<span data-ttu-id="e5066-181">Puntee en hello botón registro (big círculo rojo en la parte inferior de Hola de pantalla de bienvenida) toostart un viaje y, nuevo en tooend.</span><span class="sxs-lookup"><span data-stu-id="e5066-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Ilustración del botón de registro de hello para el seguimiento de ida y vuelta](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="e5066-183">Cada vez que inicie un recorrido, si no hay ningún dispositivo DAB, se le preguntará si desea que el simulador de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="e5066-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="e5066-184">Al final de Hola de un recorrido, botón de detención de derivación de Hola y obtener un resumen.</span><span class="sxs-lookup"><span data-stu-id="e5066-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Ejemplo de un resumen de viaje](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="e5066-186">Revise sus viajes.</span><span class="sxs-lookup"><span data-stu-id="e5066-186">Review your trips</span></span>
![Ejemplo de un viaje anterior](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="e5066-188">Revise su perfil.</span><span class="sxs-lookup"><span data-stu-id="e5066-188">Review your profile</span></span>
![Ejemplo de un perfil de conducción](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="e5066-190">Envíenos sus comentarios de prueba.</span><span class="sxs-lookup"><span data-stu-id="e5066-190">Send us your test feedback</span></span>
<span data-ttu-id="e5066-191">Ya hemos creado el punto de partida de MyDriving toohelp sus propios sistemas de IoT, por supuesto, es deseable toohear del usuario acerca de cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="e5066-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="e5066-192">Queremos saber si:</span><span class="sxs-lookup"><span data-stu-id="e5066-192">Let us know if:</span></span>

* <span data-ttu-id="e5066-193">Se enfrenta a dificultades y desafíos.</span><span class="sxs-lookup"><span data-stu-id="e5066-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="e5066-194">Hay un punto de extensión que le resulte más conveniente escenario tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5066-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="e5066-195">Buscar un tooaccomplish de manera más eficaz de ciertas necesidades.</span><span class="sxs-lookup"><span data-stu-id="e5066-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="e5066-196">Tiene cualquier sugerencia para mejorar MyDriving o esta documentación.</span><span class="sxs-lookup"><span data-stu-id="e5066-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="e5066-197">Dentro de hello MyDriving propia aplicación, puede usar mecanismo de comentarios de Hola integrado HockeyApp: en iOS y Android, simplemente asigne su teléfono un apretón o usar hello **comentarios** comando de menú.</span><span class="sxs-lookup"><span data-stu-id="e5066-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="e5066-198">Esta acción asociará automáticamente una captura de pantalla, por lo que ya sabremos de que está hablando.</span><span class="sxs-lookup"><span data-stu-id="e5066-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="e5066-199">Y si hay cualquier bloqueos indeseable, HockeyApp recopila Hola bloqueo registros tootell nos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="e5066-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="e5066-200">También puede proporcionar comentarios a través de hello [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="e5066-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="e5066-201">Asimismo puede registrar un [problema en GitHub] o dejar un comentario a continuación (edición en inglés).</span><span class="sxs-lookup"><span data-stu-id="e5066-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="e5066-202">¡Esperamos tener toohearing del usuario.</span><span class="sxs-lookup"><span data-stu-id="e5066-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5066-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5066-203">Next steps</span></span>
* <span data-ttu-id="e5066-204">Explorar hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs) toounderstand cómo hemos diseñado y compilado Hola MyDriving todo el sistema.</span><span class="sxs-lookup"><span data-stu-id="e5066-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="e5066-205">[Cree e implemente un sistema por su cuenta](iot-solution-build-system.md) con nuestros scripts de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5066-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="e5066-206">Hola [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs) también le guía a través de las áreas donde realizará Hola mayoría de las personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="e5066-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[desde GitHub]: https://github.com/Azure-Samples/MyDriving
[con Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[herramienta de análisis BAFX Products 34t5 Bluetooth OBDII]: http://www.amazon.com/gp/product/B005NLQAHS
[detector de diagnóstico y adaptador OBD ScanTool OBDLink MX Wi-Fi]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problema en GitHub]: https://github.com/Azure-Samples/MyDriving/issues
