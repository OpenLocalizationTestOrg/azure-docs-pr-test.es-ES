---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="6de25-103">Cómo tooIntegrate interacción a en Android</span><span class="sxs-lookup"><span data-stu-id="6de25-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6de25-104">Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.</span><span class="sxs-lookup"><span data-stu-id="6de25-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="6de25-105">Integración estándar</span><span class="sxs-lookup"><span data-stu-id="6de25-105">Standard integration</span></span>

<span data-ttu-id="6de25-106">Copie los archivos de recursos de alcance de hello SDK en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="6de25-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="6de25-107">Copie los archivos de Hola de hello `res/layout` carpeta ofrece Hola SDK en hello `res/layout` carpeta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6de25-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="6de25-108">Copie los archivos de Hola de hello `res/drawable` carpeta ofrece Hola SDK en hello `res/drawable` carpeta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6de25-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="6de25-109">Edite su archivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="6de25-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="6de25-110">Agregar pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="6de25-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* <span data-ttu-id="6de25-111">Notificaciones de tooreplay sistema este permiso que no se ha hecho clic en el arranque (en caso contrario, se conservará en el disco pero no se mostrarán ya, tiene en realidad tooinclude esto).</span><span class="sxs-lookup"><span data-stu-id="6de25-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="6de25-112">Especificar un icono que se usa para notificaciones (tanto en la aplicación y del sistema), copiando y editando los pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="6de25-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="6de25-113">Esta sección es **obligatoria** si planifica utilizar notificaciones del sistema al crear campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="6de25-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="6de25-114">Android impide que se muestren las notificaciones del sistema sin iconos.</span><span class="sxs-lookup"><span data-stu-id="6de25-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="6de25-115">Por lo que si se omite en esta sección, los usuarios finales no será capaz de tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="6de25-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="6de25-116">Si creas las campañas con notificaciones del sistema con la idea global, necesita hello tooadd los siguientes permisos (después de hello `</application>` etiqueta) si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="6de25-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="6de25-117">En Android M y si la aplicación está destinada al nivel de API Android 23 o superior, el permiso ``WRITE_EXTERNAL_STORAGE`` requiere la aprobación del usuario.</span><span class="sxs-lookup"><span data-stu-id="6de25-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="6de25-118">Lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="6de25-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="6de25-119">Para las notificaciones del sistema que también puede especificar en hello alcancen campaña si dispositivo Hola debe sonar o Vibrar.</span><span class="sxs-lookup"><span data-stu-id="6de25-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="6de25-120">Para toowork, tendrá que declaran Hola después permiso toomake (después de hello `</application>` etiqueta):</span><span class="sxs-lookup"><span data-stu-id="6de25-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="6de25-121">Sin este permiso, Android, impide que las notificaciones del sistema que no se muestre si ha seleccionado anillo de Hola o hello Vibrar opción en el Administrador de campaña alcanzar Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="6de25-122">Inserción nativa:</span><span class="sxs-lookup"><span data-stu-id="6de25-122">Native Push</span></span>
<span data-ttu-id="6de25-123">Ahora que ha configurado el módulo de Reach, debe tooconfigure nativo toobe tooreceive capaz de hello las campañas de inserción en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="6de25-124">Se admiten dos servicios en Android:</span><span class="sxs-lookup"><span data-stu-id="6de25-124">We support two services on Android:</span></span>

* <span data-ttu-id="6de25-125">Dispositivos de Google Play: Use [Google Cloud Messaging] por hello siguiente [cómo guía tooIntegrate GCM con interacción](mobile-engagement-android-gcm-integrate.md) guía.</span><span class="sxs-lookup"><span data-stu-id="6de25-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="6de25-126">Dispositivos de Amazon: Use [Amazon Device Messaging] por hello siguiente [cómo guía tooIntegrate ADM con interacción](mobile-engagement-android-adm-integrate.md) guía.</span><span class="sxs-lookup"><span data-stu-id="6de25-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="6de25-127">Si desea que tootarget dispositivos de Amazon y Google Play, su posibles toohave todos los datos 1 AndroidManifest.xml/APK para el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6de25-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="6de25-128">Pero, al enviar tooAmazon, puede rechazar la aplicación si encuentra el código de GCM.</span><span class="sxs-lookup"><span data-stu-id="6de25-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="6de25-129">En ese caso, debe usar varios APK.</span><span class="sxs-lookup"><span data-stu-id="6de25-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="6de25-130">**La aplicación está ahora listo tooreceive y presentación alcanzan las campañas!**</span><span class="sxs-lookup"><span data-stu-id="6de25-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="6de25-131">Cómo inserción datos toohandle</span><span class="sxs-lookup"><span data-stu-id="6de25-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="6de25-132">Integración</span><span class="sxs-lookup"><span data-stu-id="6de25-132">Integration</span></span>
<span data-ttu-id="6de25-133">Si desea que su aplicación toobe pueda inserta tooreceive datos de cobertura, tendrá que toocreate una subclase de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` y hacer referencia a él en hello `AndroidManifest.xml` archivo (entre hello `<application>` o `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="6de25-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="6de25-134">A continuación, puede invalidar hello `onDataPushStringReceived` y `onDataPushBase64Received` las devoluciones de llamada.</span><span class="sxs-lookup"><span data-stu-id="6de25-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="6de25-135">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6de25-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="6de25-136">Categoría</span><span class="sxs-lookup"><span data-stu-id="6de25-136">Category</span></span>
<span data-ttu-id="6de25-137">parámetro de categoría de Hello es opcional cuando se crea una campaña de inserción de datos y permite que los datos de toofilter inserta.</span><span class="sxs-lookup"><span data-stu-id="6de25-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="6de25-138">Esto es útil si tiene varios receptores difusión de administración de los diferentes tipos de inserciones de datos, o si desea toopush diferentes tipos de `Base64` tooidentify de datos y quiere que su tipo antes del análisis de ellos.</span><span class="sxs-lookup"><span data-stu-id="6de25-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="6de25-139">Parámetro de devolución de devoluciones de llamada</span><span class="sxs-lookup"><span data-stu-id="6de25-139">Callbacks' return parameter</span></span>
<span data-ttu-id="6de25-140">Estas son algunas directrices tooproperly identificador hello parámetro devuelto de `onDataPushStringReceived` y `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="6de25-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="6de25-141">Debe devolver un receptor de difusión `null` de devolución de llamada de hello si no sabe cómo insertar toohandle datos.</span><span class="sxs-lookup"><span data-stu-id="6de25-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="6de25-142">Debe usar Hola categoría toodetermine si el receptor difusión debe controlar la inserción de datos de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="6de25-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="6de25-143">Uno de hello difusión receptor debe devolver `true` en devolución de llamada de hello si acepta la inserción de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="6de25-144">Uno de hello difusión receptor debe devolver `false` en devolución de llamada de hello si se reconoce la inserción de datos de hello, pero descarta por cualquier motivo.</span><span class="sxs-lookup"><span data-stu-id="6de25-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="6de25-145">Por ejemplo, devolver `false` cuando Hola recibido datos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="6de25-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="6de25-146">Si una difusión receptor devuelve `true` mientras otro uno devuelve `false` para hello misma inserción de datos, el comportamiento de hello no está definido, nunca debe hacerlo.</span><span class="sxs-lookup"><span data-stu-id="6de25-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="6de25-147">tipo de valor devuelto de Hola se usa solo para las estadísticas de cobertura de hello:</span><span class="sxs-lookup"><span data-stu-id="6de25-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="6de25-148">`Replied`se incrementa si uno de los receptores de difusión de hello devuelve cualquiera `true` o `false`.</span><span class="sxs-lookup"><span data-stu-id="6de25-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="6de25-149">`Actioned`se incrementa sólo si uno de hello difusión receptores devueltos `true`.</span><span class="sxs-lookup"><span data-stu-id="6de25-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="6de25-150">Cómo las campañas de toocustomize</span><span class="sxs-lookup"><span data-stu-id="6de25-150">How toocustomize campaigns</span></span>
<span data-ttu-id="6de25-151">las campañas de toocustomize, puede modificar diseños de hello proporcionados Hola Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="6de25-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="6de25-152">Debe mantener todos los identificadores de hello usados en los diseños de Hola y mantener Hola tipos de vistas de Hola que utiliza un identificador, especialmente para las vistas de texto y las vistas de la imagen.</span><span class="sxs-lookup"><span data-stu-id="6de25-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="6de25-153">Algunas vistas son solo usa toohide o muestran las áreas, por lo que se puede cambiar su tipo.</span><span class="sxs-lookup"><span data-stu-id="6de25-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="6de25-154">Compruebe código fuente de hello si piensa toochange tipo de saludo de una vista en los diseños de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="6de25-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="6de25-155">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="6de25-155">Notifications</span></span>
<span data-ttu-id="6de25-156">Existen dos tipos de notificaciones: notificaciones del sistema y notificaciones en aplicación, las que usan distintos archivos de diseño.</span><span class="sxs-lookup"><span data-stu-id="6de25-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="6de25-157">Notificaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="6de25-157">System notifications</span></span>
<span data-ttu-id="6de25-158">notificaciones del sistema toocustomize necesita hello toouse **categorías**.</span><span class="sxs-lookup"><span data-stu-id="6de25-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="6de25-159">También puede avanzar demasiado[categorías](#categories).</span><span class="sxs-lookup"><span data-stu-id="6de25-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="6de25-160">Notificación en aplicación</span><span class="sxs-lookup"><span data-stu-id="6de25-160">In-app notifications</span></span>
<span data-ttu-id="6de25-161">De forma predeterminada, una notificación en la aplicación es una vista que es toohello agregados dinámicamente actual actividad usuario gracias toohello Android método de interfaz `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="6de25-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="6de25-162">Esto se denomina superposición de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="6de25-162">This is called a notification overlay.</span></span> <span data-ttu-id="6de25-163">Superposiciones de notificación son excelentes para una integración rápida porque no requieren toomodify cualquier diseño de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6de25-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="6de25-164">visión de hello toomodify de sus superposiciones de notificación, simplemente puede modificar archivo hello `engagement_notification_area.xml` tooyour necesita.</span><span class="sxs-lookup"><span data-stu-id="6de25-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="6de25-165">archivo hello `engagement_notification_overlay.xml` es uno que sea utilizado toocreate Hola una superposición de notificación, incluye el archivo hello `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="6de25-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="6de25-166">También se puede personalizar toosuit sus necesidades (por ejemplo, para colocar el área de notificación de hello en superposición de hello).</span><span class="sxs-lookup"><span data-stu-id="6de25-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="6de25-167">Incluya el diseño de la notificación como parte de un diseño de actividad</span><span class="sxs-lookup"><span data-stu-id="6de25-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="6de25-168">Las superposiciones son ideales para lograr una integración rápida, pero puede ser poco conveniente o tener efectos secundarios en casos especiales.</span><span class="sxs-lookup"><span data-stu-id="6de25-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="6de25-169">sistema de superposición de Hello puede personalizarse en un nivel de actividad, lo que efectos secundarios de tooprevent fácil para actividades especiales.</span><span class="sxs-lookup"><span data-stu-id="6de25-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="6de25-170">Puede decidir tooinclude nuestro diseño de notificación en la toohello gracias de diseño existente Android **incluyen** instrucción.</span><span class="sxs-lookup"><span data-stu-id="6de25-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="6de25-171">Hello aquí te mostramos un ejemplo de una modificación `ListActivity` diseño que simplemente contienen un `ListView`.</span><span class="sxs-lookup"><span data-stu-id="6de25-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="6de25-172">**Antes de la integración de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="6de25-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="6de25-173">**Después de la integración de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="6de25-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="6de25-174">En este ejemplo se agrega un contenedor primario porque diseño original de hello usando una vista de lista como elemento de nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="6de25-175">También hemos agregado `android:layout_weight="1"` toobe capaz tooadd una vista por debajo de una vista de lista configurado con `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="6de25-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="6de25-176">Hola interacción Reach SDK detecta automáticamente ese diseño de notificación de Hola se incluye en esta actividad y no agregará una superposición para esta actividad.</span><span class="sxs-lookup"><span data-stu-id="6de25-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="6de25-177">Si usas un ListActivity en la aplicación, una superposición de cobertura visible no podrá reaccionando elementos tooclicked en la vista de lista de hello ya.</span><span class="sxs-lookup"><span data-stu-id="6de25-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="6de25-178">Este es un problema conocido.</span><span class="sxs-lookup"><span data-stu-id="6de25-178">This is a known issue.</span></span> <span data-ttu-id="6de25-179">toowork solucionar este problema se recomienda tooembed diseño de notificación de hello en su propio diseño de la actividad de lista como en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="6de25-180">Deshabilitación de notificación de aplicación por actividad</span><span class="sxs-lookup"><span data-stu-id="6de25-180">Disabling application notification per activity</span></span>
<span data-ttu-id="6de25-181">Si no desea hello toobe de superposición agrega tooyour actividad y, si no incluye el diseño de la notificación de hello en un diseño propio, puede deshabilitar la superposición de Hola para esta actividad en hello `AndroidManifest.xml` agregando un `meta-data` sección, como en los siguientes Hola ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6de25-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="6de25-182"><a name="categories"></a> Categorías</span><span class="sxs-lookup"><span data-stu-id="6de25-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="6de25-183">Cuando se modifica Hola proporcionada diseños, modificar aspecto de Hola de todas las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="6de25-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="6de25-184">Las categorías permiten toodefine que distintos destino busca (posiblemente comportamientos) para las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="6de25-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="6de25-185">Las categorías pueden especificarse cuando se crea una campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="6de25-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="6de25-186">Tenga en cuenta que las categorías también permiten personalizar anuncios y sondeos, aspectos que se describen más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="6de25-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="6de25-187">tooregister un controlador de categoría para las notificaciones, debe tooadd una llamada cuando se inicializa la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6de25-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6de25-188">Lea la advertencia Hola sobre el atributo de android: proceso de hello \<android-sdk-en proceso de contratación\> Hola cómo tooIntegrate interacción en tema Android antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="6de25-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="6de25-189">Hello en el ejemplo siguiente se supone que reconoce la advertencia anterior hello y utilice una subclase de `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="6de25-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="6de25-190">Hola `MyNotifier` objeto es la implementación de Hola de controlador de categoría de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="6de25-191">Es cualquier implementación de hello `EngagementNotifier` interfaz o una subclase de la implementación predeterminada de hello: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="6de25-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="6de25-192">Tenga en cuenta que Hola notificador mismo puede controlar varias categorías, puede registrar similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6de25-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="6de25-193">implementación de categoría de tooreplace Hola predeterminada, puede registrar su implementación como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6de25-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="6de25-194">categoría de Hello actual utilizada en un controlador se pasa como un parámetro en la mayoría de los métodos se pueden reemplazar en `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="6de25-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="6de25-195">Se transmite como un parámetro `String` o de manera indirecta en un objeto `EngagementReachContent` que tiene un método `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="6de25-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="6de25-196">Puede cambiar la mayor parte del proceso de creación de notificación de hello mediante la redefinición de métodos en `EngagementDefaultNotifier`, para una personalización más avanzada sentirse tootake libre un vistazo en la documentación técnica de Hola y en código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="6de25-197">Notificación en aplicación</span><span class="sxs-lookup"><span data-stu-id="6de25-197">In-app notifications</span></span>
<span data-ttu-id="6de25-198">Si solo desea diseños alternativos de toouse para una categoría específica, puede hacerlo como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6de25-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="6de25-199">**Ejemplo de `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="6de25-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="6de25-200">Como puede ver, identificador de la vista de hello superposición es diferente de estándar de hello uno.</span><span class="sxs-lookup"><span data-stu-id="6de25-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="6de25-201">Es importante que cada diseño utilice un identificador único para las superposiciones.</span><span class="sxs-lookup"><span data-stu-id="6de25-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="6de25-202">**Ejemplo de `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="6de25-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="6de25-203">Como puede ver, identificador de la vista de área de notificación de hello es diferente de estándar de hello uno.</span><span class="sxs-lookup"><span data-stu-id="6de25-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="6de25-204">Es importante que cada diseño utilice un identificador único para las áreas de notificación.</span><span class="sxs-lookup"><span data-stu-id="6de25-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="6de25-205">Este sencillo ejemplo de categoría hace que las notificaciones de aplicación (o en la aplicación) aparece en la parte superior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="6de25-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="6de25-206">No se cambió identificadores estándar Hola usados en el área de notificación de hello propio.</span><span class="sxs-lookup"><span data-stu-id="6de25-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="6de25-207">Si desea que toochange que, tener hello tooredefine `EngagementDefaultNotifier.prepareInAppArea` método.</span><span class="sxs-lookup"><span data-stu-id="6de25-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="6de25-208">Se recomienda toolook en la documentación técnica de Hola y en código fuente de Hola de `EngagementNotifier` y `EngagementDefaultNotifier` si desea que este nivel de personalización avanzada.</span><span class="sxs-lookup"><span data-stu-id="6de25-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="6de25-209">Notificaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="6de25-209">System notifications</span></span>
<span data-ttu-id="6de25-210">Extendiendo `EngagementDefaultNotifier`, puede invalidar `onNotificationPrepared` notificación de hello tooalter que se preparó implementación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="6de25-211">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6de25-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="6de25-212">En este ejemplo realiza una notificación del sistema para un contenido que se muestra como un evento en curso cuando se utiliza la categoría "en curso" Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="6de25-213">Si desea que hello toobuild `Notification` objeto desde el principio, puede devolver `false` toohello método y llame al método `notify` usted mismo en hello `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="6de25-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="6de25-214">En ese caso es importante que mantenga un `contentIntent`, `deleteIntent` y Hola utilizado por el identificador de notificación `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="6de25-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="6de25-215">El siguiente es un ejemplo de una implementación de ese tipo correcta:</span><span class="sxs-lookup"><span data-stu-id="6de25-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="6de25-216">Anuncios solo de notificación</span><span class="sxs-lookup"><span data-stu-id="6de25-216">Notification only announcements</span></span>
<span data-ttu-id="6de25-217">Hello administración de hello haga clic en una anuncio solo puede personalizarse mediante la invalidación de notificación `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify preparado `Intent`.</span><span class="sxs-lookup"><span data-stu-id="6de25-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="6de25-218">Con este método permite marcas de hello tootune fácilmente.</span><span class="sxs-lookup"><span data-stu-id="6de25-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="6de25-219">Por ejemplo tooadd hello `SINGLE_TOP` marca:</span><span class="sxs-lookup"><span data-stu-id="6de25-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="6de25-220">Para los usuarios de contratación heredados, tenga en cuenta que las notificaciones del sistema sin ninguna acción dirección URL ahora se inicia aplicación hello si estaba en segundo plano, por lo que puede llamar a este método con un anuncio sin dirección URL de acción.</span><span class="sxs-lookup"><span data-stu-id="6de25-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="6de25-221">Debe considerar al personalizar la intención de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="6de25-222">También puede implementar `EngagementNotifier.executeNotifAnnouncementAction` desde cero.</span><span class="sxs-lookup"><span data-stu-id="6de25-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="6de25-223">Ciclo de vida de notificación</span><span class="sxs-lookup"><span data-stu-id="6de25-223">Notification life cycle</span></span>
<span data-ttu-id="6de25-224">Cuando se usa la categoría predeterminada de hello, se llaman a algunos métodos de ciclo de vida en hello `EngagementReachInteractiveContent` tooreport estadísticas y actualización Hola campaña el estado del objeto:</span><span class="sxs-lookup"><span data-stu-id="6de25-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="6de25-225">Cuando se muestra en la aplicación o colocar en la barra de estado de hello notificación de hello, Hola `displayNotification` se llama al método (que notifica estadísticas) por `EngagementReachAgent` si `handleNotification` devuelve `true`.</span><span class="sxs-lookup"><span data-stu-id="6de25-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="6de25-226">Si se descarta la notificación de hello, Hola `exitNotification` método se llama, se notifica la estadística y ahora se pueden procesar las campañas siguientes.</span><span class="sxs-lookup"><span data-stu-id="6de25-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="6de25-227">Si se hace clic en la notificación de hello, `actionNotification` es llama, se notifican estadísticas y se inicia el intento de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="6de25-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="6de25-228">Si la implementación de `EngagementNotifier` omisiones Hola comportamiento predeterminado, tendrá toocall estos métodos de ciclo de vida por usted mismo.</span><span class="sxs-lookup"><span data-stu-id="6de25-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="6de25-229">Hello en los ejemplos siguientes muestra algunos casos donde se omite el comportamiento predeterminado de hello:</span><span class="sxs-lookup"><span data-stu-id="6de25-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="6de25-230">No se extienden `EngagementDefaultNotifier`, por ejemplo, se implementa el control de categoría desde cero.</span><span class="sxs-lookup"><span data-stu-id="6de25-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="6de25-231">Para las notificaciones del sistema, reemplazó hello `onNotificationPrepared` y modificado `contentIntent` o `deleteIntent` en hello `Notification` objeto.</span><span class="sxs-lookup"><span data-stu-id="6de25-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="6de25-232">Para las notificaciones de la aplicación, reemplazó `prepareInAppArea`, ser al menos seguro toomap `actionNotification` tooone de los controles de I.U.</span><span class="sxs-lookup"><span data-stu-id="6de25-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="6de25-233">Si `handleNotification` inicia una excepción, Hola contenido se elimina y `dropContent` se llama.</span><span class="sxs-lookup"><span data-stu-id="6de25-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="6de25-234">Esto se informa en las estadísticas y ahora es posible procesar las siguientes campañas.</span><span class="sxs-lookup"><span data-stu-id="6de25-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="6de25-235">Anuncios y sondeos</span><span class="sxs-lookup"><span data-stu-id="6de25-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="6de25-236">Diseños</span><span class="sxs-lookup"><span data-stu-id="6de25-236">Layouts</span></span>
<span data-ttu-id="6de25-237">Puede modificar hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` y `engagement_poll.xml` archivos toocustomize anuncios de texto, sondeos y anuncios de web.</span><span class="sxs-lookup"><span data-stu-id="6de25-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="6de25-238">Estos archivos comparten dos diseños comunes para el área de título de Hola y área del botón Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="6de25-239">diseño de Hola de título de hello es `engagement_content_title.xml` y utiliza Hola epónimo archivos con estas características para el fondo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="6de25-240">Hello diseño de botones de acción y salir de hello es `engagement_button_bar.xml` y utiliza Hola epónimo archivos con estas características para el fondo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="6de25-241">En un sondeo, Hola diseño pregunta y sus opciones son exagerar dinámicamente mediante varias veces hello `engagement_question.xml` archivo de diseño para resolver dudas de Hola y Hola `engagement_choice.xml` archivo de opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="6de25-242">Categorías</span><span class="sxs-lookup"><span data-stu-id="6de25-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="6de25-243">Diseños alternativos</span><span class="sxs-lookup"><span data-stu-id="6de25-243">Alternate layouts</span></span>
<span data-ttu-id="6de25-244">Al igual que las notificaciones, categoría de la campaña de hello puede ser toohave usado diseños alternativos para los sondeos y anuncios.</span><span class="sxs-lookup"><span data-stu-id="6de25-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="6de25-245">Por ejemplo, toocreate una categoría de un anuncio de texto, puede ampliar `EngagementTextAnnouncementActivity` y hacer referencia a él hello `AndroidManifest.xml` archivo:</span><span class="sxs-lookup"><span data-stu-id="6de25-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="6de25-246">Tenga en cuenta esa categoría de hello en el intento de Hola se utiliza el filtro de diferencia de hello toomake con actividad de anuncio de Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6de25-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="6de25-247">Hola Reach SDK usa actividad derecho de hello sistema intención tooresolve Hola para una categoría específica y recurre en la categoría de hello predeterminado si no se pudo resolver Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="6de25-248">Tendrá que tooimplement `MyCustomTextAnnouncementActivity`, si simplemente desea toochange Hola diseño (pero mantener Hola mismos identificadores de vista), solo tienen clase de hello toodefine como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6de25-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="6de25-249">categoría de tooreplace Hola predeterminada de los anuncios de texto, reemplace simplemente `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` por su implementación.</span><span class="sxs-lookup"><span data-stu-id="6de25-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="6de25-250">Los anuncios web y los sondeos se pueden personalizar de manera similar.</span><span class="sxs-lookup"><span data-stu-id="6de25-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="6de25-251">Para anuncios web también puede extender `EngagementWebAnnouncementActivity` y declarar su actividad en hello `AndroidManifest.xml` al igual que en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6de25-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="6de25-252">Para los sondeos puede ampliar `EngagementPollActivity` y declarar su hello en `AndroidManifest.xml` como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6de25-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="6de25-253">Implementación desde cero</span><span class="sxs-lookup"><span data-stu-id="6de25-253">Implementation from scratch</span></span>
<span data-ttu-id="6de25-254">Puede implementar categorías de tus actividades de anuncio (y sondeo) sin tener que ampliar uno de hello `Engagement*Activity` las clases proporcionadas por Hola Reach SDK.</span><span class="sxs-lookup"><span data-stu-id="6de25-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="6de25-255">Esto es útil por ejemplo si desea toodefine un diseño que no usa Hola mismo vistas como diseños estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="6de25-256">Al igual que para la personalización avanzada de notificación, se recomienda toolook en el código fuente de Hola de implementación estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="6de25-257">Estas son algunas cosas tookeep en mente: alcance iniciará actividad hello con un propósito específico (filtro intención de correspondiente toohello) junto con un parámetro adicional que es el identificador de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="6de25-258">tooretrieve Hola objeto de contenido que contienen campos de Hola que especificó al crear Hola de campaña en el sitio web de Hola puede hacer esto:</span><span class="sxs-lookup"><span data-stu-id="6de25-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="6de25-259">Para las estadísticas, debería notificar es mostrar el contenido de Hola Hola `onResume` eventos:</span><span class="sxs-lookup"><span data-stu-id="6de25-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="6de25-260">A continuación, no olvide toocall o `actionContent(this)` o `exitContent(this)` en el objeto de contenido de hello antes de actividad hello entra en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="6de25-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="6de25-261">Si no llama a `actionContent` o `exitContent`, no se envían las estadísticas (es decir, ningún análisis en campaña Hola) y más importante aún, Hola campañas siguientes no será informadas hasta que se reinicie el proceso de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6de25-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="6de25-262">Orientación u otros cambios de configuración puede realizar Hola código difícil toodetermine si actividad hello entra en segundo plano o no, Hola hace de implementación estándar seguro contenido Hola se notifica como salido si usuario Hola deja actividad hello (ya sea mediante la al presionar `HOME` o `BACK`) pero no si cambia la orientación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6de25-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="6de25-263">Aquí es parte interesante de Hola de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="6de25-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="6de25-264">Como puede ver, si llama a `actionContent(this)` , a continuación, finaliza la actividad de hello, `exitContent(this)` puede llamar de forma segura sin tener ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="6de25-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
