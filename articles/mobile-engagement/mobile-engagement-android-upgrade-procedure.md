---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
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
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="4b593-103">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="4b593-103">Upgrade procedures</span></span>
<span data-ttu-id="4b593-104">Si ya ha integrado una versión anterior de nuestro SDK en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="4b593-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="4b593-105">Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4b593-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="4b593-106">Por ejemplo, si migra desde 1.4.0 too1.6.0 tiene toofirst siga Hola "de 1.4.0 too1.5.0" procedimiento, a continuación, Hola "de 1.5.0 too1.6.0" procedimiento.</span><span class="sxs-lookup"><span data-stu-id="4b593-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="4b593-107">Cualquier versión de Hola se actualiza desde, tiene hello tooreplace `mobile-engagement-VERSION.jar` con hello uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="4b593-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="4b593-108">Desde 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="4b593-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="4b593-109">Este paso puede realizarse realmente en cualquier versión de Hola SDK, es una mejora de seguridad al integrar las actividades de alcance.</span><span class="sxs-lookup"><span data-stu-id="4b593-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="4b593-110">Ahora debe agregar `exported="false"` tooall alcance actividades.</span><span class="sxs-lookup"><span data-stu-id="4b593-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="4b593-111">Las actividades de cobertura deben ser ahora similares a esta en `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="4b593-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-too410"></a><span data-ttu-id="4b593-112">Desde 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="4b593-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="4b593-113">Hola SDK ahora identificador nuevo modelo de permisos de M Android.</span><span class="sxs-lookup"><span data-stu-id="4b593-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="4b593-114">Si usa las características de ubicación o notificaciones de panorama general, lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="4b593-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="4b593-115">Además toohello al nuevo modelo de permisos, ahora se admite la configuración de características de ubicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4b593-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="4b593-116">Estamos siga siendo compatibles con parámetros para la ubicación del manifiesto de hello pero ahora está en desuso.</span><span class="sxs-lookup"><span data-stu-id="4b593-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="4b593-117">las secciones siguientes de hello remove de configuración de en tiempo de ejecución de toouse, desde su ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="4b593-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="4b593-118">y leer [Esto actualiza procedimiento](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuración de tiempo de ejecución en su lugar.</span><span class="sxs-lookup"><span data-stu-id="4b593-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="4b593-119">Desde 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="4b593-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="4b593-120">Inserción nativa</span><span class="sxs-lookup"><span data-stu-id="4b593-120">Native push</span></span>
<span data-ttu-id="4b593-121">Inserción nativa (GCM/ADM) ahora también se utiliza para las notificaciones en aplicación por lo que debe configurar credenciales de inserción nativa de Hola para cualquier tipo de campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="4b593-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="4b593-122">Si aún no lo hizo, siga [este procedimiento](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="4b593-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="4b593-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4b593-123">AndroidManifest.xml</span></span>
<span data-ttu-id="4b593-124">Se modificó la integración de Reach en ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="4b593-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="4b593-125">Reemplazar esto:</span><span class="sxs-lookup"><span data-stu-id="4b593-125">Replace this:</span></span>

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

<span data-ttu-id="4b593-126">Por</span><span class="sxs-lookup"><span data-stu-id="4b593-126">By</span></span>

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

<span data-ttu-id="4b593-127">Posiblemente, ahora hay una pantalla de carga al hacer clic en un anuncio (con texto y contenido web) o una encuesta.</span><span class="sxs-lookup"><span data-stu-id="4b593-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="4b593-128">Tienes tooadd esto para esos toowork campañas en 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="4b593-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="4b593-129">Recursos</span><span class="sxs-lookup"><span data-stu-id="4b593-129">Resources</span></span>
<span data-ttu-id="4b593-130">Incrustar Hola nueva `res/layout/engagement_loading.xml` archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4b593-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="4b593-131">De 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="4b593-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="4b593-132">Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4b593-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="4b593-133">Si va a migrar desde una versión anterior, consulte hello Capptain sitio web toomigrate too2.4.0 en primer lugar y, a continuación, aplicar Hola siguiendo el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="4b593-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b593-134">Capptain e interacción móvil son no Hola mismos servicios y Hola procedimiento que se indica a continuación solo destaca cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="4b593-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="4b593-135">Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores.</span><span class="sxs-lookup"><span data-stu-id="4b593-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="4b593-136">Archivo JAR</span><span class="sxs-lookup"><span data-stu-id="4b593-136">JAR file</span></span>
<span data-ttu-id="4b593-137">Sustituya `capptain.jar` por `mobile-engagement-VERSION.jar` en su carpeta `libs`.</span><span class="sxs-lookup"><span data-stu-id="4b593-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="4b593-138">Archivos de recursos</span><span class="sxs-lookup"><span data-stu-id="4b593-138">Resource files</span></span>
<span data-ttu-id="4b593-139">Cada archivo de recursos que se proporciona (precedida por `capptain_`) se toobe reemplazado por hello nuevos (con el prefijo `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="4b593-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="4b593-140">Si ha personalizado los archivos, tendrá que toore-aplicar la personalización en nuevos archivos de hello, **todos los identificadores de Hola Hola en archivos de recursos también ha cambiado el nombre**.</span><span class="sxs-lookup"><span data-stu-id="4b593-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="4b593-141">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="4b593-141">Application ID</span></span>
<span data-ttu-id="4b593-142">Ahora interacción usa un identificadores de conexión cadena tooconfigure Hola SDK como identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4b593-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="4b593-143">Tiene toouse `EngagementAgent.init` método en la actividad del iniciador similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b593-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="4b593-144">cadena de conexión de Hello para la aplicación se muestra en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b593-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="4b593-145">Elimine cualquier llamada`CapptainAgent.configure` como `EngagementAgent.init` reemplaza a ese método.</span><span class="sxs-lookup"><span data-stu-id="4b593-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="4b593-146">Hola `appId` ya no se puede configurar mediante `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="4b593-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="4b593-147">Quite esta sección de su `AndroidManifest.xml` si la tiene:</span><span class="sxs-lookup"><span data-stu-id="4b593-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="4b593-148">API de Java</span><span class="sxs-lookup"><span data-stu-id="4b593-148">Java API</span></span>
<span data-ttu-id="4b593-149">Cada clase de Java de nuestro SDK de llamada tooany tiene toobe cambiar el nombre; Por ejemplo, `CapptainAgent.getInstance(this)` debe cambiarse `EngagementAgent.getInstance(this)`, `extends CapptainActivity` debe cambiarse `extends EngagementActivity` etcetera...</span><span class="sxs-lookup"><span data-stu-id="4b593-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="4b593-150">Si se integra con los archivos de preferencias de agente de forma predeterminada, nombre de archivo predeterminado de hello es ahora `engagement.agent` y clave de hello es `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="4b593-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="4b593-151">Al crear anuncios web, Hola Javascript enlazador es ahora `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="4b593-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="4b593-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4b593-152">AndroidManifest.xml</span></span>
<span data-ttu-id="4b593-153">Ha ocurrido un lote de cambios, ya no se comparte el servicio de hello y una gran cantidad de destinatarios ya no son exportables.</span><span class="sxs-lookup"><span data-stu-id="4b593-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="4b593-154">declaración de servicio de Hello ahora es más sencillo; Quitar filtro de intención de Hola y todos los metadatos dentro de él y agregar `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="4b593-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="4b593-155">Además de todo lo que es la contratación de toouse cuyo nombre ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="4b593-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="4b593-156">Ahora se parece a esto:</span><span class="sxs-lookup"><span data-stu-id="4b593-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="4b593-157">Cuando desee que los registros de pruebas tooenable, Hola metadatos ahora ha sido movido toohello etiqueta de la aplicación y se ha cambiado el nombre:</span><span class="sxs-lookup"><span data-stu-id="4b593-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="4b593-158">Todos los demás datos meta simplemente ha cambiado el nombre, esta es la lista completa de hello (evidentemente rename solo Hola que usas):</span><span class="sxs-lookup"><span data-stu-id="4b593-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="4b593-159">Seguimiento de Google Play y SmartAd se ha quitado del SDK sólo tiene tooremove esto sin reemplazo:</span><span class="sxs-lookup"><span data-stu-id="4b593-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="4b593-160">las actividades de cobertura de Hola se declaran ahora similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b593-160">hello Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="4b593-161">Si tiene actividades personalizadas de alcance, necesita ya sea solo toochange Hola acciones intención toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` o `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="4b593-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="4b593-162">Hello difusión receptores han cambiado de nombre, además de agregamos ahora `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="4b593-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="4b593-163">Esta es Hola lista completa de destinatarios de hello con nueva especificación de hello, (evidentemente rename solo Hola que usas):</span><span class="sxs-lookup"><span data-stu-id="4b593-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

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

<span data-ttu-id="4b593-164">Se ha quitado la seguimiento receptor, por lo que tendrá tooremove en esta sección:</span><span class="sxs-lookup"><span data-stu-id="4b593-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="4b593-165">Tenga en cuenta que la declaración de Hola de su implementación de hello difusión receptor **EngagementMessageReceiver** ha cambiado en hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="4b593-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="4b593-166">Esto es porque Hola API toosend y quite XMPP arbitrario mensajes desde entidades XMPP arbitrarias y Hola API toosend y recibir mensajes entre los dispositivos se han quitado.</span><span class="sxs-lookup"><span data-stu-id="4b593-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="4b593-167">Por lo tanto, también tiene hello toodelete siguiendo las devoluciones de llamada desde el **EngagementMessageReceiver** implementación:</span><span class="sxs-lookup"><span data-stu-id="4b593-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="4b593-168">y</span><span class="sxs-lookup"><span data-stu-id="4b593-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="4b593-169">luego elimine toda llamada en **EngagementAgent** para:</span><span class="sxs-lookup"><span data-stu-id="4b593-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="4b593-170">y</span><span class="sxs-lookup"><span data-stu-id="4b593-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="4b593-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="4b593-171">Proguard</span></span>
<span data-ttu-id="4b593-172">Configuración proguard puede verse afectado por la reconfiguración de marca, Hola ahora se parecido a las reglas:</span><span class="sxs-lookup"><span data-stu-id="4b593-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

