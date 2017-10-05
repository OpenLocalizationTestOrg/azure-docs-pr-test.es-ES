---
title: "Integración del SDK de Android para Azure Mobile Engagement"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="9739b-103">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="9739b-103">Upgrade procedures</span></span>
<span data-ttu-id="9739b-104">Si ya integró una versión anterior de nuestro SDK en la aplicación, debería tener en cuenta los siguientes puntos a la hora de actualizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="9739b-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="9739b-105">Es posible que tenga que seguir varios procedimientos si se perdió varias versiones del SDK.</span><span class="sxs-lookup"><span data-stu-id="9739b-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="9739b-106">Por ejemplo, si migra de la versión 1.4.0 a la versión 1.6.0, primero tiene que seguir el procedimiento "de la versión 1.4.0 a la versión 1.5.0" y, a continuación, el procedimiento "de la versión 1.5.0 a la versión 1.6.0".</span><span class="sxs-lookup"><span data-stu-id="9739b-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="9739b-107">Sea cual sea la versión desde la que actualice, debe reemplazar `mobile-engagement-VERSION.jar` por el nuevo.</span><span class="sxs-lookup"><span data-stu-id="9739b-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="9739b-108">De 4.2.0 a 4.2.1</span><span class="sxs-lookup"><span data-stu-id="9739b-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="9739b-109">Este paso puede realizarse realmente en cualquier versión del SDK, es una mejora de seguridad al integrar actividades de cobertura.</span><span class="sxs-lookup"><span data-stu-id="9739b-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="9739b-110">Ahora debe agregar `exported="false"` a todas las actividades de cobertura.</span><span class="sxs-lookup"><span data-stu-id="9739b-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="9739b-111">Las actividades de cobertura deben ser ahora similares a esta en `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="9739b-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="9739b-112">De 4.0.0 a 4.1.0</span><span class="sxs-lookup"><span data-stu-id="9739b-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="9739b-113">El SDK ahora controla el nuevo modelo de permiso desde Android M.</span><span class="sxs-lookup"><span data-stu-id="9739b-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="9739b-114">Si usa las características de ubicación o notificaciones de panorama general, lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="9739b-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="9739b-115">Además del nuevo modelo de permiso, ahora se admiten características de ubicación de configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9739b-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="9739b-116">Seguimos siendo compatibles con los parámetros de manifiesto de ubicación, pero ahora está en desuso.</span><span class="sxs-lookup"><span data-stu-id="9739b-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="9739b-117">Para usar la configuración de tiempo de ejecución, quite las siguientes secciones de ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="9739b-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="9739b-118">y lea [este procedimiento actualizado](mobile-engagement-android-integrate-engagement.md#location-reporting) para usar la configuración de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9739b-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="9739b-119">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="9739b-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="9739b-120">Inserción nativa</span><span class="sxs-lookup"><span data-stu-id="9739b-120">Native push</span></span>
<span data-ttu-id="9739b-121">La inserción nativa (GCM/ADM) ahora también se usa para notificaciones dentro de la aplicación, por lo que debe configurar las credenciales de inserción nativas para cualquier tipo de campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="9739b-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="9739b-122">Si aún no lo hizo, siga [este procedimiento](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="9739b-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="9739b-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9739b-123">AndroidManifest.xml</span></span>
<span data-ttu-id="9739b-124">Se modificó la integración de Reach en ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="9739b-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="9739b-125">Reemplazar esto:</span><span class="sxs-lookup"><span data-stu-id="9739b-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="9739b-126">Por</span><span class="sxs-lookup"><span data-stu-id="9739b-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
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

<span data-ttu-id="9739b-127">Posiblemente, ahora hay una pantalla de carga al hacer clic en un anuncio (con texto y contenido web) o una encuesta.</span><span class="sxs-lookup"><span data-stu-id="9739b-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="9739b-128">Debe agregar esto para que las campañas funcionen en 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="9739b-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="9739b-129">Recursos</span><span class="sxs-lookup"><span data-stu-id="9739b-129">Resources</span></span>
<span data-ttu-id="9739b-130">Inserte el nuevo archivo `res/layout/engagement_loading.xml` en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="9739b-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="9739b-131">De 2.4.0 a 3.0.0</span><span class="sxs-lookup"><span data-stu-id="9739b-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="9739b-132">A continuación se describe cómo migrar una integración del SDK desde el servicio Capptain que ofrece Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9739b-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="9739b-133">Si va a migrar desde una versión anterior, consulte el sitio web de Capptain para migrar a 2.4.0 en primer lugar y luego aplique el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9739b-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9739b-134">Capptain y Mobile Engagement no son los mismos servicios, y el procedimiento que se indica a continuación destaca únicamente cómo migrar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="9739b-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="9739b-135">La migración del SDK en la aplicación NO migrará los datos desde los servidores Capptain a los servidores Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9739b-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="9739b-136">Archivo JAR</span><span class="sxs-lookup"><span data-stu-id="9739b-136">JAR file</span></span>
<span data-ttu-id="9739b-137">Sustituya `capptain.jar` por `mobile-engagement-VERSION.jar` en su carpeta `libs`.</span><span class="sxs-lookup"><span data-stu-id="9739b-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="9739b-138">Archivos de recursos</span><span class="sxs-lookup"><span data-stu-id="9739b-138">Resource files</span></span>
<span data-ttu-id="9739b-139">Cada archivo de recursos que hemos proporcionado (con el prefijo `capptain_`) se debe reemplazar por los nuevos (con el prefijo `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="9739b-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="9739b-140">Si ha personalizado esos archivos, debe volver a aplicar la personalización en los archivos nuevos y **también se cambió el nombre de todos los identificadores en los archivos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="9739b-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="9739b-141">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="9739b-141">Application ID</span></span>
<span data-ttu-id="9739b-142">Engagement ahora usa una cadena de conexión para configurar los identificadores del SDK, como el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9739b-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="9739b-143">Debe usar el método `EngagementAgent.init` en la actividad del iniciador, de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9739b-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="9739b-144">La cadena de conexión de la aplicación se muestra en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9739b-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="9739b-145">Quite toda llamada a `CapptainAgent.configure`, puesto que `EngagementAgent.init` reemplaza ese método.</span><span class="sxs-lookup"><span data-stu-id="9739b-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="9739b-146">El `appId` ya no se puede configurar mediante `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="9739b-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="9739b-147">Quite esta sección de su `AndroidManifest.xml` si la tiene:</span><span class="sxs-lookup"><span data-stu-id="9739b-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="9739b-148">API de Java</span><span class="sxs-lookup"><span data-stu-id="9739b-148">Java API</span></span>
<span data-ttu-id="9739b-149">Cada llamada a cualquier clase Java de nuestro SDK se ha de cambiar de nombre, por ejemplo `CapptainAgent.getInstance(this)` debe tener ahora el nombre `EngagementAgent.getInstance(this)`, `extends CapptainActivity` debe tener ahora el nombre `extends EngagementActivity` etc...</span><span class="sxs-lookup"><span data-stu-id="9739b-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="9739b-150">Si estuviera integrado con archivos de preferencia del agente predeterminados, el nombre de archivo predeterminado ahora es `engagement.agent` y la clave es `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="9739b-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="9739b-151">Al crear anuncios web, el enlazador de Javascript ahora es `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="9739b-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="9739b-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9739b-152">AndroidManifest.xml</span></span>
<span data-ttu-id="9739b-153">Muchos cambios se han producido ahí, el servicio ya no se comparte y muchos receptores ya no son exportables.</span><span class="sxs-lookup"><span data-stu-id="9739b-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="9739b-154">La declaración de servicio ahora es más simple: quite el filtro de intento y todos los metadatos que contenga y agregue `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="9739b-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="9739b-155">Además, todo cambia de nombre para usar Engagement.</span><span class="sxs-lookup"><span data-stu-id="9739b-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="9739b-156">Ahora se parece a esto:</span><span class="sxs-lookup"><span data-stu-id="9739b-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="9739b-157">Cuando desee habilitar los registros de prueba, ahora los metadatos se movieron a la etiqueta de aplicación y ahora se llaman:</span><span class="sxs-lookup"><span data-stu-id="9739b-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="9739b-158">Todos los demás metadatos han cambiado de nombre; esta es la lista completa (naturalmente, cambie de nombre solo los que use):</span><span class="sxs-lookup"><span data-stu-id="9739b-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="9739b-159">El seguimiento de SmartAd y Google Play se quitó del SDK; solo debe quitar esto sin reemplazarlo:</span><span class="sxs-lookup"><span data-stu-id="9739b-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="9739b-160">Las actividades de cobertura se declaran ahora de esta forma:</span><span class="sxs-lookup"><span data-stu-id="9739b-160">The Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="9739b-161">Si tiene actividades de cobertura personalizadas, solo necesita cambiar las acciones preventivas para que coincidan con `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` o con `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="9739b-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="9739b-162">Los receptores de difusión han cambiado de nombre; además, ahora nosotros agregamos `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="9739b-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="9739b-163">Esta es la lista completa de los receptores con su nueva especificación (por supuesto, cambie el nombre solo de las que usa):</span><span class="sxs-lookup"><span data-stu-id="9739b-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="9739b-164">Se quitó el receptor de seguimiento, por lo que debe quitar esta sección:</span><span class="sxs-lookup"><span data-stu-id="9739b-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="9739b-165">Tenga en cuenta que la declaración de su implementación del receptor de difusión **EngagementMessageReceiver** ha cambiado en `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="9739b-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="9739b-166">Esto se debe a que la API para enviar y eliminar mensajes XMPP arbitrarios de entidades XMPP arbitrarias y la API para enviar y recibir mensajes entre dispositivos se han eliminado.</span><span class="sxs-lookup"><span data-stu-id="9739b-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="9739b-167">Por lo tanto, también tiene que eliminar las siguientes devoluciones de llamada de su implementación de **EngagementMessageReceiver** :</span><span class="sxs-lookup"><span data-stu-id="9739b-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="9739b-168">y</span><span class="sxs-lookup"><span data-stu-id="9739b-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="9739b-169">luego elimine toda llamada en **EngagementAgent** para:</span><span class="sxs-lookup"><span data-stu-id="9739b-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="9739b-170">y</span><span class="sxs-lookup"><span data-stu-id="9739b-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="9739b-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="9739b-171">Proguard</span></span>
<span data-ttu-id="9739b-172">La configuración de Proguard se puede ver afectada por la renovación de la marca; las reglas ahora se ven de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9739b-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

