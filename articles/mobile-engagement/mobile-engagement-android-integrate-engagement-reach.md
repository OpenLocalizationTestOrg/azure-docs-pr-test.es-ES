---
title: "Integración del SDK de Android para Azure Mobile Engagement"
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
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="5ec87-103">Integración de cobertura para Engagement en Android</span><span class="sxs-lookup"><span data-stu-id="5ec87-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ec87-104">Debe seguir el procedimiento de integración descrito en el documento Integración de Engagement en Android antes de seguir con esta guía.</span><span class="sxs-lookup"><span data-stu-id="5ec87-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="5ec87-105">Integración estándar</span><span class="sxs-lookup"><span data-stu-id="5ec87-105">Standard integration</span></span>

<span data-ttu-id="5ec87-106">Copie los archivos de recursos de cobertura desde el SDK en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="5ec87-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="5ec87-107">Copie los archivos desde la carpeta `res/layout` proporcionada con el SDK a la carpeta `res/layout` de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="5ec87-108">Copie los archivos desde la carpeta `res/drawable` proporcionada con el SDK a la carpeta `res/drawable` de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="5ec87-109">Edite su archivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="5ec87-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="5ec87-110">Agregue la siguiente sección (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="5ec87-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="5ec87-111">Necesita este permiso para reproducir notificaciones del sistema en las que no se hizo clic durante el arranque (de lo contrario, se mantendrán en el disco, pero no volverán a mostrarse. Realmente debe incluir esto).</span><span class="sxs-lookup"><span data-stu-id="5ec87-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="5ec87-112">Para especificar un icono utilizado para las notificaciones (tanto en las notificaciones de aplicación y del sistema), copie y edite la siguiente sección (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="5ec87-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="5ec87-113">Esta sección es **obligatoria** si planifica utilizar notificaciones del sistema al crear campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="5ec87-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="5ec87-114">Android impide que se muestren las notificaciones del sistema sin iconos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="5ec87-115">Por tanto, si omite esta sección, los usuarios finales no podrán recibirlas.</span><span class="sxs-lookup"><span data-stu-id="5ec87-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="5ec87-116">Si crea campañas con notificaciones del sistema con imagen global, deberá agregar los siguientes permisos (después de la etiqueta `</application>` ) si no se encuentran presentes:</span><span class="sxs-lookup"><span data-stu-id="5ec87-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="5ec87-117">En Android M y si la aplicación está destinada al nivel de API Android 23 o superior, el permiso ``WRITE_EXTERNAL_STORAGE`` requiere la aprobación del usuario.</span><span class="sxs-lookup"><span data-stu-id="5ec87-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="5ec87-118">Lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="5ec87-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="5ec87-119">En el caso de las notificaciones del sistema, también puede especificar en la campaña de cobertura si el dispositivo debe sonar y/o vibrar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="5ec87-120">Para que funcione, debe asegurarse de haber declarado el siguiente permiso (después de la etiqueta `</application>` ):</span><span class="sxs-lookup"><span data-stu-id="5ec87-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="5ec87-121">Sin este permiso, Android impide que se muestren notificaciones del sistema si marca la opción de sonar o vibrar en el administrador de la campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="5ec87-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="5ec87-122">Inserción nativa:</span><span class="sxs-lookup"><span data-stu-id="5ec87-122">Native Push</span></span>
<span data-ttu-id="5ec87-123">Ahora que ha configurado el módulo Reach, deberá configurar la inserción nativa para poder recibir las campañas en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="5ec87-124">Se admiten dos servicios en Android:</span><span class="sxs-lookup"><span data-stu-id="5ec87-124">We support two services on Android:</span></span>

* <span data-ttu-id="5ec87-125">Dispositivos de Google Play: use [Google Cloud Messaging] siguiendo la guía [Integración de GCM con Mobile Engagement](mobile-engagement-android-gcm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="5ec87-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="5ec87-126">Dispositivos Amazon: use [Amazon Device Messaging] siguiendo la guía [Integración de ADM con Engagement](mobile-engagement-android-adm-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="5ec87-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="5ec87-127">Si desea orientarse a dispositivos de Amazon y de Google Play, es posible que todo esté dentro de un AndroidManifest.xml/APK para desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="5ec87-128">Pero al enviar a Amazon, es posible que se rechace la aplicación si se encuentra código de GCM.</span><span class="sxs-lookup"><span data-stu-id="5ec87-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="5ec87-129">En ese caso, debe usar varios APK.</span><span class="sxs-lookup"><span data-stu-id="5ec87-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="5ec87-130">**Ahora su aplicación está lista para recibir y mostrar campañas de cobertura.**</span><span class="sxs-lookup"><span data-stu-id="5ec87-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="5ec87-131">Control de inserción de datos</span><span class="sxs-lookup"><span data-stu-id="5ec87-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="5ec87-132">Integración</span><span class="sxs-lookup"><span data-stu-id="5ec87-132">Integration</span></span>
<span data-ttu-id="5ec87-133">Si desea que su aplicación reciba inserciones de datos de cobertura, debe crear una subclase de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` y hacer referencia a ella en el archivo `AndroidManifest.xml` (entre las etiquetas `<application>` y/o `</application>`):</span><span class="sxs-lookup"><span data-stu-id="5ec87-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="5ec87-134">Luego puede invalidar las devoluciones de llamada `onDataPushStringReceived` y `onDataPushBase64Received`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="5ec87-135">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="5ec87-136">Categoría</span><span class="sxs-lookup"><span data-stu-id="5ec87-136">Category</span></span>
<span data-ttu-id="5ec87-137">El parámetro de categoría es opcional cuando se crea una campaña de inserción de datos y permite filtrar los datos que inserta.</span><span class="sxs-lookup"><span data-stu-id="5ec87-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="5ec87-138">Esto es útil si tiene varios receptores de difusión que controlan distintos tipos de inserciones de datos, o bien, si desea insertar distintos tipos de datos `Base64` y desea identificar su tipo antes de analizarlos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="5ec87-139">Parámetro de devolución de devoluciones de llamada</span><span class="sxs-lookup"><span data-stu-id="5ec87-139">Callbacks' return parameter</span></span>
<span data-ttu-id="5ec87-140">Estas son algunas directrices para manejar correctamente el parámetro de devolución de `onDataPushStringReceived` y `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="5ec87-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="5ec87-141">Un receptor de difusión debiera devolver `null` en la devolución de llamada si no sabe cómo controlar una inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="5ec87-142">Debe usar la categoría para determina si el receptor de difusión debe controlar o no la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="5ec87-143">Uno de los receptores de difusión debe devolver `true` en la devolución de llamada si acepta la inserción de datos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="5ec87-144">Uno de los receptores de difusión debe devolver `false` en la devolución de llamada si reconoce la inserción de datos, pero la descarta por cualquier motivo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="5ec87-145">Por ejemplo, devuelve `false` cuando los datos recibidos no son válidos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="5ec87-146">Si un receptor de difusión devuelve `true` mientras que otro devuelve `false` para la misma inserción de datos, el comportamiento es indefinido; nunca debe hacerlo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="5ec87-147">El tipo de devolución se usa solo para las estadísticas de cobertura:</span><span class="sxs-lookup"><span data-stu-id="5ec87-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="5ec87-148">`Replied` aumenta si uno de los receptores de difusión devolvió `true` o `false`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="5ec87-149">`Actioned` aumenta solo si uno de los receptores de difusión devolvió `true`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="5ec87-150">Personalización de las campañas</span><span class="sxs-lookup"><span data-stu-id="5ec87-150">How to customize campaigns</span></span>
<span data-ttu-id="5ec87-151">Para personalizar campañas, puede modificar los diseños proporcionados en el SDK de cobertura.</span><span class="sxs-lookup"><span data-stu-id="5ec87-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="5ec87-152">Debe conservar todos los identificadores usados en los diseños y los tipos de las vistas que usa un identificador, especialmente para vistas de texto y vistas de imagen.</span><span class="sxs-lookup"><span data-stu-id="5ec87-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="5ec87-153">Algunas vistas solo se utilizan para ocultar o mostrar áreas, por tanto, es posible que se cambie su tipo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="5ec87-154">Compruebe el código fuente si intenta cambiar el tipo de una vista de los diseños proporcionados.</span><span class="sxs-lookup"><span data-stu-id="5ec87-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="5ec87-155">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="5ec87-155">Notifications</span></span>
<span data-ttu-id="5ec87-156">Existen dos tipos de notificaciones: notificaciones del sistema y notificaciones en aplicación, las que usan distintos archivos de diseño.</span><span class="sxs-lookup"><span data-stu-id="5ec87-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="5ec87-157">Notificaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="5ec87-157">System notifications</span></span>
<span data-ttu-id="5ec87-158">Para personalizar las notificaciones del sistema, debe usar las **categorías**.</span><span class="sxs-lookup"><span data-stu-id="5ec87-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="5ec87-159">Puede ir a [Categorías](#categories).</span><span class="sxs-lookup"><span data-stu-id="5ec87-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="5ec87-160">Notificación en aplicación</span><span class="sxs-lookup"><span data-stu-id="5ec87-160">In-app notifications</span></span>
<span data-ttu-id="5ec87-161">De manera predeterminada, una notificación en aplicación es una vista que se agrega de manera dinámica a la interfaz de usuario de actividad actual gracias al método Android `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="5ec87-162">Esto se denomina superposición de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-162">This is called a notification overlay.</span></span> <span data-ttu-id="5ec87-163">Las superposiciones de notificación son ideales para una integración rápida, debido a que no requieren que modifique ningún diseño en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="5ec87-164">Para modificar el aspecto de las superposiciones de notificación, puede simplemente modificar el archivo `engagement_notification_area.xml` según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="5ec87-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="5ec87-165">El archivo `engagement_notification_overlay.xml` es el que se usa para crear una superposición de notificación; incluye el archivo `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="5ec87-166">También puede personalizarla para ajustarse a sus necesidades (como para posicionar el área de notificación dentro de la superposición).</span><span class="sxs-lookup"><span data-stu-id="5ec87-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="5ec87-167">Incluya el diseño de la notificación como parte de un diseño de actividad</span><span class="sxs-lookup"><span data-stu-id="5ec87-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="5ec87-168">Las superposiciones son ideales para lograr una integración rápida, pero puede ser poco conveniente o tener efectos secundarios en casos especiales.</span><span class="sxs-lookup"><span data-stu-id="5ec87-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="5ec87-169">El sistema de superposición se puede personalizar en el nivel de una actividad, para que sea fácil impedir los efectos secundarios para actividades especiales.</span><span class="sxs-lookup"><span data-stu-id="5ec87-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="5ec87-170">Puede decidir incluir nuestro diseño de notificación en su diseño existente gracias a la instrucción **include** de Android.</span><span class="sxs-lookup"><span data-stu-id="5ec87-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="5ec87-171">El siguiente es un ejemplo de un diseño `ListActivity` modificado que contiene solo una `ListView`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="5ec87-172">**Antes de la integración de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5ec87-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="5ec87-173">**Después de la integración de Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5ec87-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="5ec87-174">En este ejemplo agregamos un contenedor principal, debido a que el diseño original usó una vista de lista como el elemento de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="5ec87-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="5ec87-175">También agregamos `android:layout_weight="1"` para poder agregar una vista debajo de una vista de lista configurada con `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="5ec87-176">El SDK de cobertura para Engagement detecta automáticamente que el diseño de notificación está incluido en esta actividad y no agregará una superposición para esta actividad.</span><span class="sxs-lookup"><span data-stu-id="5ec87-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="5ec87-177">Si usa una ListActivity en su aplicación, una superposición de cobertura visible impedirá que vuelva a reaccionar ante los elementos en los que se ha hecho clic en la vista de lista.</span><span class="sxs-lookup"><span data-stu-id="5ec87-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="5ec87-178">Este es un problema conocido.</span><span class="sxs-lookup"><span data-stu-id="5ec87-178">This is a known issue.</span></span> <span data-ttu-id="5ec87-179">Para solucionar este problema, le recomendamos que incruste el diseño de notificación en su propio diseño de actividad de lista, como en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="5ec87-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="5ec87-180">Deshabilitación de notificación de aplicación por actividad</span><span class="sxs-lookup"><span data-stu-id="5ec87-180">Disabling application notification per activity</span></span>
<span data-ttu-id="5ec87-181">Si no desea agregar la superposición a su actividad y no desea incluir el diseño de notificación en su propio diseño, puede deshabilitar la superposición para esta actividad en el `AndroidManifest.xml` al agregar una sección `meta-data`, como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="5ec87-182"><a name="categories"></a> Categorías</span><span class="sxs-lookup"><span data-stu-id="5ec87-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="5ec87-183">Cuando modifica los diseños proporcionados, modifica el aspecto de todas las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="5ec87-184">Las categorías permiten definir varios destinos objetivo (posiblemente comportamientos) para las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="5ec87-185">Las categorías pueden especificarse cuando se crea una campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="5ec87-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="5ec87-186">Tenga en cuenta que las categorías también permiten personalizar anuncios y sondeos, aspectos que se describen más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="5ec87-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="5ec87-187">Para registrar un controlador de categorías para las notificaciones, debe agregar una llamada cuando se inicializa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ec87-188">Lea la advertencia sobre el atributo android:process \<android-sdk-engagement-process\> en el tema Integración de Engagement en Android antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="5ec87-189">El siguiente ejemplo supone que reconoció la advertencia anterior y que usa una subclase de `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="5ec87-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="5ec87-190">El objeto `MyNotifier` es la implementación del controlador de categorías de notificación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="5ec87-191">Es una implementación de la interfaz `EngagementNotifier` o una subclase de la implementación predeterminada: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="5ec87-192">Observe que el mismo notificador puede controlar varias categorías. Puede registrarlas de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="5ec87-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="5ec87-193">Para reemplazar la implementación de categoría predeterminada, puede registrar su implementación como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

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

<span data-ttu-id="5ec87-194">La categoría actual usada en un controlador se transmite como un parámetro en la mayoría de los métodos que puede invalidar en `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="5ec87-195">Se transmite como un parámetro `String` o de manera indirecta en un objeto `EngagementReachContent` que tiene un método `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="5ec87-196">Puede cambiar la mayor parte del proceso de creación de notificaciones si redefine los métodos en `EngagementDefaultNotifier`; si desea obtener una apariencia de personalización más avanzada, revise la documentación técnica y el código fuente.</span><span class="sxs-lookup"><span data-stu-id="5ec87-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="5ec87-197">Notificación en aplicación</span><span class="sxs-lookup"><span data-stu-id="5ec87-197">In-app notifications</span></span>
<span data-ttu-id="5ec87-198">Si solo desea usar diseños alternativos para una categoría específica, puede implementar esto como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

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

<span data-ttu-id="5ec87-199">**Ejemplo de `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="5ec87-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="5ec87-200">Como puede ver, el identificador de vista de superposición es distinto al estándar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="5ec87-201">Es importante que cada diseño utilice un identificador único para las superposiciones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="5ec87-202">**Ejemplo de `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="5ec87-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="5ec87-203">Como puede ver, el identificador de vista del área de notificación es distinto del estándar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="5ec87-204">Es importante que cada diseño utilice un identificador único para las áreas de notificación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="5ec87-205">Este ejemplo simple de categoría crea notificaciones de aplicación (o en aplicación) que se muestran en la parte superior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="5ec87-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="5ec87-206">No cambiamos los identificadores estándar que se usan en el área de notificación misma.</span><span class="sxs-lookup"><span data-stu-id="5ec87-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="5ec87-207">Si desea cambiar eso, debe redefinir el método `EngagementDefaultNotifier.prepareInAppArea` .</span><span class="sxs-lookup"><span data-stu-id="5ec87-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="5ec87-208">Se recomienda consultar la documentación técnica y el código fuente de `EngagementNotifier` y `EngagementDefaultNotifier` si desea este nivel de personalización avanzada.</span><span class="sxs-lookup"><span data-stu-id="5ec87-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="5ec87-209">Notificaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="5ec87-209">System notifications</span></span>
<span data-ttu-id="5ec87-210">Al extender `EngagementDefaultNotifier`, puede invalidar `onNotificationPrepared` para modificar la notificación que se preparó mediante la implementación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5ec87-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="5ec87-211">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="5ec87-212">Este ejemplo crea una notificación del sistema para un contenido que se muestra como un evento en curso cuando se utiliza la categoría "en curso".</span><span class="sxs-lookup"><span data-stu-id="5ec87-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="5ec87-213">Si desea crear el objeto `Notification` desde cero, puede devolver `false` al método y llamar a `notify` usted mismo en `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="5ec87-214">En ese caso, es importante que conserve un `contentIntent`, un `deleteIntent` y el identificador de notificación que utiliza `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="5ec87-215">El siguiente es un ejemplo de una implementación de ese tipo correcta:</span><span class="sxs-lookup"><span data-stu-id="5ec87-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="5ec87-216">Anuncios solo de notificación</span><span class="sxs-lookup"><span data-stu-id="5ec87-216">Notification only announcements</span></span>
<span data-ttu-id="5ec87-217">La administración del clic en un anuncio de solo notificación se puede personalizar al anular `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` para modificar el `Intent` preparado.</span><span class="sxs-lookup"><span data-stu-id="5ec87-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="5ec87-218">Usar este método le permite ajusta fácilmente las marcas.</span><span class="sxs-lookup"><span data-stu-id="5ec87-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="5ec87-219">Por ejemplo, para agregar la marca `SINGLE_TOP` :</span><span class="sxs-lookup"><span data-stu-id="5ec87-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="5ec87-220">En el caso de los usuarios de Engagement heredado, observe que las notificaciones del sistema sin dirección URL de acción ahora inicia la aplicación si estaba en segundo plano, por tanto, es posible llamar a este método con un anuncio sin una dirección URL de acción.</span><span class="sxs-lookup"><span data-stu-id="5ec87-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="5ec87-221">Debe considerar eso al personalizar el intento.</span><span class="sxs-lookup"><span data-stu-id="5ec87-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="5ec87-222">También puede implementar `EngagementNotifier.executeNotifAnnouncementAction` desde cero.</span><span class="sxs-lookup"><span data-stu-id="5ec87-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="5ec87-223">Ciclo de vida de notificación</span><span class="sxs-lookup"><span data-stu-id="5ec87-223">Notification life cycle</span></span>
<span data-ttu-id="5ec87-224">Al utilizar la categoría predeterminada, se llama a algunos métodos de ciclo de vida en el objeto `EngagementReachInteractiveContent` para mostrar estadísticas y actualizar el estado de la campaña:</span><span class="sxs-lookup"><span data-stu-id="5ec87-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="5ec87-225">Cuando la notificación se muestra en la aplicación o se pone en la barra de estado, se llama al método `displayNotification` (que informa las estadísticas) mediante `EngagementReachAgent` si `handleNotification` devuelve `true`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="5ec87-226">Si se descarta la notificación, se llama al método `exitNotification`, se notifica la estadística y ahora se pueden procesar las campañas siguientes.</span><span class="sxs-lookup"><span data-stu-id="5ec87-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="5ec87-227">Si se hace clic en la notificación, se llama a `actionNotification` , se informa la estadística y se inicie el intento asociado.</span><span class="sxs-lookup"><span data-stu-id="5ec87-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="5ec87-228">Si su implementación de pasa por alto `EngagementNotifier` el comportamiento predeterminado, tiene que llamar a estos métodos de ciclo de vida por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="5ec87-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="5ec87-229">Los ejemplos siguientes muestran algunos casos donde se omite el comportamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="5ec87-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="5ec87-230">No se extienden `EngagementDefaultNotifier`, por ejemplo, se implementa el control de categoría desde cero.</span><span class="sxs-lookup"><span data-stu-id="5ec87-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="5ec87-231">En el caso de las notificaciones del sistema, anuló la `onNotificationPrepared` y modificó el `contentIntent` o el `deleteIntent` en el objeto `Notification`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="5ec87-232">En el caso de las notificaciones en aplicación, anuló `prepareInAppArea`; asegúrese de asignar, al menos `actionNotification`, a uno de sus controles de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="5ec87-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="5ec87-233">Si `handleNotification` arroja una excepción, se elimina el contenido y se llama a `dropContent`.</span><span class="sxs-lookup"><span data-stu-id="5ec87-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="5ec87-234">Esto se informa en las estadísticas y ahora es posible procesar las siguientes campañas.</span><span class="sxs-lookup"><span data-stu-id="5ec87-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="5ec87-235">Anuncios y sondeos</span><span class="sxs-lookup"><span data-stu-id="5ec87-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="5ec87-236">Diseños</span><span class="sxs-lookup"><span data-stu-id="5ec87-236">Layouts</span></span>
<span data-ttu-id="5ec87-237">Puede modificar los archivos `engagement_text_announcement.xml`, `engagement_web_announcement.xml` y `engagement_poll.xml` para personalizar anuncios de texto, anuncios web y sondeos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="5ec87-238">Estos archivos comparten dos diseños comunes para el área de título y el área de botones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="5ec87-239">El diseño del título es `engagement_content_title.xml` y usa el archivo dibujable epónimo para el segundo plano.</span><span class="sxs-lookup"><span data-stu-id="5ec87-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="5ec87-240">El diseño de los botones de acción y salida es `engagement_button_bar.xml` y usa el archivo dibujable epónimo para el segundo plano.</span><span class="sxs-lookup"><span data-stu-id="5ec87-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="5ec87-241">En un sondeo, el diseño de la pregunta y sus opciones se inflan de manera dinámica usando varias veces el archivo de diseño `engagement_question.xml` para las preguntas y el archivo `engagement_choice.xml` para las opciones.</span><span class="sxs-lookup"><span data-stu-id="5ec87-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="5ec87-242">Categorías</span><span class="sxs-lookup"><span data-stu-id="5ec87-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="5ec87-243">Diseños alternativos</span><span class="sxs-lookup"><span data-stu-id="5ec87-243">Alternate layouts</span></span>
<span data-ttu-id="5ec87-244">Como con las notificaciones, la categoría de la campaña puede utilizarse para tener diseños alternativos para los anuncios y sondeos.</span><span class="sxs-lookup"><span data-stu-id="5ec87-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="5ec87-245">Por ejemplo, para crear una categoría para un anuncio de texto, puede extender `EngagementTextAnnouncementActivity` y hacer referencia a él en el archivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="5ec87-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="5ec87-246">Observe que la categoría del filtro de intento se usa para marcar la diferencia con la actividad de anuncio predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5ec87-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="5ec87-247">El SDK de cobertura usa el sistema de intento para resolver la actividad adecuada para una categoría específica y vuelve a la categoría predeterminada si la resolución no se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="5ec87-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="5ec87-248">Luego debe implementar `MyCustomTextAnnouncementActivity`; si solo desea cambiar el diseño (pero mantener los mismos identificadores de vista), solo debe definir la clase como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5ec87-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="5ec87-249">Para reemplazar la categoría predeterminada de anuncios de texto, solo reemplace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` por su implementación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="5ec87-250">Los anuncios web y los sondeos se pueden personalizar de manera similar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="5ec87-251">En el caso de los anuncios web, puede extender `EngagementWebAnnouncementActivity` y declarar su actividad en el `AndroidManifest.xml`, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ec87-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="5ec87-252">En el caso de los sondeos, puede extender `EngagementPollActivity` y declarar su actividad en el `AndroidManifest.xml`, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ec87-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="5ec87-253">Implementación desde cero</span><span class="sxs-lookup"><span data-stu-id="5ec87-253">Implementation from scratch</span></span>
<span data-ttu-id="5ec87-254">Puede implementar categorías para sus actividades de anuncio (y sondeo) sin extender una de las clases `Engagement*Activity` proporcionadas por el SDK de cobertura.</span><span class="sxs-lookup"><span data-stu-id="5ec87-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="5ec87-255">Esto resulta útil, por ejemplo, si desea definir un diseño que no utiliza las mismas vistas que los diseños estándar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="5ec87-256">Al igual que para la personalización de notificación avanzada, se recomienda mirar el código fuente de la implementación estándar.</span><span class="sxs-lookup"><span data-stu-id="5ec87-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="5ec87-257">A continuación se indican algunas cosas que es necesario tener en cuenta: Cobertura iniciará la actividad con un intento específico (correspondiente al filtro de intento), más un parámetro adicional, que es el identificador de contenido.</span><span class="sxs-lookup"><span data-stu-id="5ec87-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="5ec87-258">Para recuperar el objeto de contenido que contiene los campos que especificó al crear la campaña en el sitio web, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ec87-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

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

<span data-ttu-id="5ec87-259">En el caso de las estadísticas, debe informar que el contenido se muestra en el evento `onResume`:</span><span class="sxs-lookup"><span data-stu-id="5ec87-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="5ec87-260">Luego, no olvide de llamar a `actionContent(this)` o a `exitContent(this)` en el objeto de contenido antes de que la actividad pase a segundo plano.</span><span class="sxs-lookup"><span data-stu-id="5ec87-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="5ec87-261">Si no llama a `actionContent` o a `exitContent`, no se enviarán las estadísticas (es decir, no habrá análisis en la campaña) y, lo que es más importante, las siguientes campañas no se notificarán hasta que se reinicie el proceso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="5ec87-262">Los cambios de orientación u otros cambios de configuración pueden hacer que el código sea complicado como para determinar si la actividad pasa o no al segundo plano; la implementación estándar se asegura de que se informe el contenido al salir si el usuario deja la actividad (ya sea presionando `HOME` o `BACK`), pero no si cambia la orientación.</span><span class="sxs-lookup"><span data-stu-id="5ec87-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="5ec87-263">Esta es la parte interesante de la implementación:</span><span class="sxs-lookup"><span data-stu-id="5ec87-263">Here is the interesting part of the implementation:</span></span>

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
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="5ec87-264">Como puede ver, si llamó a `actionContent(this)` y luego finalizó la actividad, se puede llamar a `exitContent(this)` de manera segura sin que tenga ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="5ec87-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="5ec87-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="5ec87-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="5ec87-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="5ec87-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
